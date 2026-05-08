import { google, gmail_v1 } from 'googleapis';
import { OAuth2Client } from 'google-auth-library';

export const GMAIL_SCOPES = [
  'https://www.googleapis.com/auth/gmail.readonly',
  'https://www.googleapis.com/auth/gmail.modify',
];

export interface GmailCredentials {
  access_token: string;
  refresh_token?: string;
  expiry_date?: number;
}

export interface ParsedEmail {
  messageId: string;
  threadId: string;
  subject: string;
  from: string;
  date: string;
  snippet: string;
  body: string;
  htmlBody?: string;
  retailer: string | null;
  orderNumber: string | null;
  purchaseDate: string | null;
  productName: string | null;
  price: number | null;
  currency: string;
  orderStatus: string | null;
  confidence: number;
  parsedAt: string;
}

export interface GmailMessage {
  id: string;
  threadId: string;
  subject: string;
  from: string;
  date: string;
  snippet: string;
  body: string;
  htmlBody?: string;
}

function createOAuth2Client(): OAuth2Client {
  return new google.auth.OAuth2(
    process.env.GMAIL_CLIENT_ID,
    process.env.GMAIL_CLIENT_SECRET,
    process.env.GMAIL_REDIRECT_URI
  );
}

export function getAuthUrl(userId: string): string {
  const oauth2Client = createOAuth2Client();
  return oauth2Client.generateAuthUrl({
    access_type: 'offline',
    scope: GMAIL_SCOPES,
    state: userId,
    prompt: 'consent',
  });
}

export async function exchangeCode(code: string): Promise<{
  credentials: GmailCredentials;
  refreshToken: string;
}> {
  const oauth2Client = createOAuth2Client();
  const { tokens } = await oauth2Client.getToken(code);
  oauth2Client.setCredentials(tokens);

  return {
    credentials: {
      access_token: tokens.access_token!,
      refresh_token: tokens.refresh_token,
      expiry_date: tokens.expiry_date,
    },
    refreshToken: tokens.refresh_token || '',
  };
}

export function createGmailClient(credentials: GmailCredentials): gmail_v1.Gmail {
  const oauth2Client = createOAuth2Client();
  oauth2Client.setCredentials(credentials);
  return google.gmail({ version: 'v1', auth: oauth2Client });
}

export const gmailClient = {
  async listEmails(params: {
    query?: string;
    maxResults?: number;
    labelIds?: string[];
  }): Promise<{ id: string; threadId: string }[]> {
    const gmail = createGmailClient(getStoredCredentials());
    const { data } = await gmail.users.messages.list({
      userId: 'me',
      q: params.query || 'is:inbox',
      maxResults: params.maxResults || 10,
      labelIds: params.labelIds,
    });

    return (data.messages || []).map((m) => ({
      id: m.id!,
      threadId: m.threadId!,
    }));
  },

  async getEmail(messageId: string): Promise<GmailMessage> {
    const gmail = createGmailClient(getStoredCredentials());
    const { data } = await gmail.users.messages.get({
      userId: 'me',
      id: messageId,
      format: 'full',
    });

    const headers = data.payload?.headers || [];
    const getHeader = (name: string) =>
      headers.find((h) => h.name?.toLowerCase() === name.toLowerCase())?.value || '';

    // Extract body
    let body = '';
    let htmlBody: string | undefined;

    function getBody(part: gmail_v1.Schema$MessagePart): string {
      if (!part) return '';
      if (part.body?.data) {
        const decoded = Buffer.from(part.body.data, 'base64').toString('utf-8');
        if (part.mimeType === 'text/plain') body = decoded;
        if (part.mimeType === 'text/html') htmlBody = decoded;
        return decoded;
      }
      if (part.parts) {
        return part.parts.map(getBody).join('\n');
      }
      return '';
    }

    getBody(data.payload!);

    return {
      id: data.id!,
      threadId: data.threadId!,
      subject: getHeader('Subject'),
      from: getHeader('From'),
      date: getHeader('Date'),
      snippet: data.snippet || '',
      body,
      htmlBody,
    };
  },

  async getRecentOrders(params: {
    retailer?: string;
    daysBack?: number;
    maxResults?: number;
  }): Promise<GmailMessage[]> {
    const daysBack = params.daysBack || 90;
    const cutoff = new Date();
    cutoff.setDate(cutoff.getDate() - daysBack);

    const retailerQueries: Record<string, string> = {
      amazon: 'from:amazon.com subject:order OR subject:confirmation',
      zara: 'from:zara.com OR from:orders@zara.com',
      hm: 'from:hm.com OR from:order@hm.com',
      bestbuy: 'from:bestbuy.com subject:order OR subject:confirmation',
      target: 'from:target.com OR from:orders@target.com',
      walmart: 'from:walmart.com OR from:order@walmart.com',
      nordstrom: 'from:nordstrom.com OR from:order@nordstrom.com',
      asos: 'from:asos.com OR from:orders@asos.com',
      general: 'subject:order confirmation OR subject:your order',
    };

    const query = params.retailer
      ? retailerQueries[params.retailer] || params.retailer
      : Object.values(retailerQueries).join(' OR ');

    const afterQuery = `after:${cutoff.toISOString().split('T')[0]}`.replace(/-/g, '/');

    const messages = await this.listEmails({
      query: `(${query}) (${afterQuery})`,
      maxResults: params.maxResults || 50,
    });

    const emails: GmailMessage[] = [];
    for (const msg of messages) {
      try {
        const email = await this.getEmail(msg.id);
        emails.push(email);
      } catch (e) {
        console.error(`Failed to fetch email ${msg.id}:`, e);
      }
    }

    return emails;
  },
};

// Placeholder — replace with real credential storage
function getStoredCredentials(): GmailCredentials {
  // In production: fetch from database keyed by userId
  return {
    access_token: process.env.GMAIL_ACCESS_TOKEN || '',
    refresh_token: process.env.GMAIL_REFRESH_TOKEN,
    expiry_date: undefined,
  };
}
