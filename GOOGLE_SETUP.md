# Google Sign-In Setup Guide

This document explains how to configure Google OAuth 2.0 authentication and Google Drive integration for the OAK Invoicing application.

---

## Prerequisites

- A Google account
- Access to Google Cloud Console

---

## Step 1: Create a Google Cloud Project

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Click **Select a Project** → **New Project**
3. Enter project name: `OAK Invoicing`
4. Click **Create**

---

## Step 2: Enable Required APIs

1. In your project, go to **APIs & Services** → **Library**
2. Search for and enable:
   - **Google Drive API**
   - **Google Identity Services API** (may be enabled by default)

---

## Step 3: Configure OAuth Consent Screen

1. Go to **APIs & Services** → **OAuth consent screen**
2. Select **External** user type
3. Click **Create**
4. Fill in required fields:
   - **App name**: OAK Invoicing
   - **User support email**: Your email
   - **Developer contact email**: Your email
5. Click **Save and Continue**
6. On **Scopes** page, click **Add or Remove Scopes**
7. Add the following scope:
   - `https://www.googleapis.com/auth/drive.file`
8. Click **Save and Continue**
9. Add test users (your email address)
10. Click **Save and Continue**

---

## Step 4: Create OAuth 2.0 Credentials

### Create OAuth Client ID

1. Go to **APIs & Services** → **Credentials**
2. Click **+ Create Credentials** → **OAuth client ID**
3. Select **Web application**
4. Set name: `OAK Invoicing Web Client`
5. Add **Authorized JavaScript origins**:
   - `http://localhost:8080` (for local development)
   - `http://127.0.0.1:8080` (for local development)
   - Your production domain (e.g., `https://yourdomain.com`)
6. Add **Authorized redirect URIs**:
   - `http://localhost:8080` (for local development)
   - Your production domain (e.g., `https://yourdomain.com`)
7. Click **Create**
8. **Copy the Client ID** - you'll need this!

### Create API Key

1. Click **+ Create Credentials** → **API Key**
2. **Copy the API Key** - you'll need this!
3. Click **Restrict Key** (recommended)
4. Under **API restrictions**, select **Restrict key**
5. Select **Google Drive API**
6. Click **Save**

---

## Step 5: Update Application Configuration

1. Open `index.html` in a text editor
2. Find the `GOOGLE_CONFIG` object (around line 483):

```javascript
const GOOGLE_CONFIG = {
    CLIENT_ID: 'YOUR_GOOGLE_CLIENT_ID_HERE.apps.googleusercontent.com',
    API_KEY: 'YOUR_API_KEY_HERE',
    DISCOVERY_DOCS: ['https://www.googleapis.com/discovery/v1/apis/drive/v3/rest'],
    SCOPES: 'https://www.googleapis.com/auth/drive.file',
    FOLDER_NAME: 'OAK_Invoicing_Data'
};
```

3. Replace `YOUR_GOOGLE_CLIENT_ID_HERE` with your Client ID from Step 4
4. Replace `YOUR_API_KEY_HERE` with your API Key from Step 4
5. Save the file

**Example:**
```javascript
const GOOGLE_CONFIG = {
    CLIENT_ID: '123456789-abcdefghijklmnop.apps.googleusercontent.com',
    API_KEY: 'AIzaSyABC123DEF456GHI789JKL012MNO345PQR',
    DISCOVERY_DOCS: ['https://www.googleapis.com/discovery/v1/apis/drive/v3/rest'],
    SCOPES: 'https://www.googleapis.com/auth/drive.file',
    FOLDER_NAME: 'OAK_Invoicing_Data'
};
```

---

## Step 6: Test the Application

### Local Testing

1. Install http-server (if not already installed):
   ```bash
   npm install
   ```

2. Start the server:
   ```bash
   npm start
   ```

3. Open your browser and navigate to:
   ```
   http://localhost:8080
   ```

4. You should see the Google Sign-In button
5. Click **Sign in with Google**
6. Authorize the application
7. After successful sign-in, you should see your profile and the invoice interface

### Test Cloud Sync

1. Create a new invoice
2. Click **Save to Drive**
3. Check your Google Drive - you should see a folder named `OAK_Invoicing_Data`
4. Inside, you'll find your Excel file with invoice data
5. Open the app on another device (or incognito window)
6. Sign in with the same Google account
7. Your invoice should automatically load!

---

## Step 7: Deploy to Production

When deploying to production:

1. Update **Authorized JavaScript origins** in Google Cloud Console:
   - Add your production domain (e.g., `https://invoicing.yourcompany.com`)

2. Update **Authorized redirect URIs**:
   - Add your production domain

3. If using OAuth consent screen in **External** mode:
   - Submit for verification if you want users outside your organization to access it
   - Or keep it in testing mode and manually add users as test users

---

## Troubleshooting

### "Sign-in button doesn't appear"
- Check browser console for errors
- Ensure Google Identity Services script is loaded
- Verify CLIENT_ID is correct

### "Access blocked: Authorization Error"
- Ensure your domain is added to Authorized JavaScript origins
- Check that the OAuth consent screen is configured
- Add your email as a test user

### "Failed to save to Google Drive"
- Verify Google Drive API is enabled
- Check API Key is correct
- Ensure you granted the required permissions during sign-in

### "Invalid API key"
- Regenerate API key in Google Cloud Console
- Make sure API restrictions include Google Drive API

---

## Security Notes

- **Never commit your credentials to version control**
- Consider using environment variables for production
- The `drive.file` scope only allows access to files created by the app
- Users' invoice data is stored in their own Google Drive
- Tokens are stored in sessionStorage (cleared when browser is closed)

---

## Features

✅ **Google Sign-In** - Secure authentication with Google accounts
✅ **Auto-sync to Google Drive** - Invoices automatically saved to user's Drive
✅ **Multi-device access** - Access invoices from any device
✅ **Automatic folder management** - Creates `OAK_Invoicing_Data` folder
✅ **Session persistence** - Stays logged in during browser session
✅ **Offline fallback** - Can still use local Excel files without sign-in

---

## Next Steps

1. Set up your Google Cloud project
2. Get your credentials
3. Update the configuration
4. Test locally
5. Deploy to production
6. Start invoicing from anywhere!

For support, refer to the [AUDIT_REPORT.md](./AUDIT_REPORT.md) for code quality and security information.
