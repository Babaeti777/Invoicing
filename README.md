# OAK Invoicing — Modern Excel-Based Tool

A professional invoicing application with **Google Sign-In** and **cloud synchronization** via Google Drive. Create, manage, and access your invoices from any device!

---

## 🚀 New Features (Latest Update)

### Google Sign-In & Multi-Device Access
- ✅ **Secure Google Authentication** - Sign in with your Google account
- ✅ **Cloud Sync** - Automatically save invoices to Google Drive
- ✅ **Multi-Device Support** - Access your invoices from any device
- ✅ **Auto-Load** - Latest invoice automatically loads when you sign in
- ✅ **Session Persistence** - Stay signed in during your browser session

### Security & Bug Fixes
- ✅ **XSS Protection** - HTML escaping to prevent script injection
- ✅ **Input Validation** - Prevents negative values in calculations
- ✅ **Fixed Attachments** - File attachment feature now works correctly
- ✅ **Improved Error Handling** - Better error messages and recovery

---

## 📋 Features

### Invoice Management
- Create **Invoices** and **Estimates**
- Invoice numbering and status tracking
- Multiple line items with quantities and rates
- **Sub-items support** for detailed breakdowns
- Payment tracking with history
- Custom adjustments (Bond, Overhead, Profit percentages)
- Tax calculation
- Balance due calculation

### Storage & Sync
- **Google Drive Integration** - Cloud storage for multi-device access
- **Excel Export/Import** - Download invoices as .xlsx files
- Multi-sheet workbook structure
- File attachments (stored in Excel)
- Automatic backup to Google Drive

### UI/UX
- **Dark/Light Mode** - Toggle theme with persistence
- **Responsive Design** - Works on mobile, tablet, and desktop
- **Print to PDF** - Professional PDF generation
- PDF stamps (Paid, Overdue, Void, Draft, Confidential)
- Real-time calculations
- Toast notifications

---

## 🛠️ Setup

### Quick Start (Local)

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd Invoicing
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Start the server:**
   ```bash
   npm start
   ```

4. **Open in browser:**
   ```
   http://localhost:8080
   ```

### Google Sign-In Setup (Required for Cloud Sync)

To enable Google Sign-In and cloud synchronization, you need to:

1. Create a Google Cloud project
2. Enable Google Drive API
3. Create OAuth 2.0 credentials
4. Update the application configuration

**👉 See [GOOGLE_SETUP.md](./GOOGLE_SETUP.md) for detailed instructions**

---

## 📖 Usage

### Without Google Sign-In (Offline Mode)
- Create invoices locally
- Save/load Excel files from your computer
- All data stored in downloaded Excel files

### With Google Sign-In (Cloud Mode)
1. Click **Sign in with Google**
2. Authorize the application
3. Create invoices - they auto-save to Google Drive
4. Access from any device by signing in

### Creating an Invoice

1. Select **Invoice** or **Estimate**
2. Enter invoice number and client details
3. Add line items (click "+ Add Item")
4. Use sub-items for detailed breakdowns
5. Add adjustments (Bond, Overhead, Profit) if needed
6. Set tax percentage
7. Click **Save to Drive** (if signed in) or **Save Local Excel**

### Multi-Device Workflow

**On Device 1:**
1. Sign in with Google
2. Create an invoice
3. Click "Save to Drive"

**On Device 2:**
1. Sign in with the same Google account
2. Invoice automatically loads!
3. Make edits and save again

---

## 📁 File Structure

```
Invoicing/
├── index.html           # Main application (all-in-one file)
├── package.json         # Node.js dependencies
├── README.md           # This file
├── GOOGLE_SETUP.md     # Google OAuth setup guide
└── AUDIT_REPORT.md     # Code audit and security report
```

---

## 🔐 Security

- **XSS Protection**: All user input is sanitized
- **Secure Auth**: Uses Google OAuth 2.0
- **Limited Scope**: Only accesses files created by the app
- **Session Storage**: Tokens stored securely, cleared on close
- **No Backend**: All processing happens client-side

See [AUDIT_REPORT.md](./AUDIT_REPORT.md) for detailed security analysis.

---

## 🧪 Data Format

Invoices are stored in multi-sheet Excel workbooks with the following structure:

- **Records** - Invoice metadata and totals
- **LineItems** - Line items for each invoice
- **SubItems** - Sub-items for line items
- **Payments** - Payment history
- **Attachments** - File attachments (base64 encoded)
- **Meta** - Schema version and export info

**Schema Version:** 1.5

---

## 💡 Tips

- **Auto-sync**: Changes are automatically saved when you click "Save to Drive"
- **Offline work**: You can still use local Excel files without signing in
- **Multiple records**: One Excel file can contain multiple invoices
- **Print to PDF**: Use your browser's print function (Ctrl+P / Cmd+P)
- **Dark mode**: Toggle theme with the moon/sun icon
- **Attachments**: Upload files that will be embedded in the Excel file

---

## 🐛 Known Issues

- Large attachments increase Excel file size significantly
- Google OAuth requires setup (see GOOGLE_SETUP.md)
- Requires modern browser with JavaScript enabled

---

## 🚀 Future Enhancements

- [ ] Automatic backup intervals
- [ ] Invoice templates
- [ ] Email integration
- [ ] Multi-currency support
- [ ] Recurring invoices
- [ ] Analytics dashboard
- [ ] Client management
- [ ] Configurable company information

---

## 📝 License

This project is provided as-is for business use.

---

## 🆘 Support

For issues or questions:

1. Check [GOOGLE_SETUP.md](./GOOGLE_SETUP.md) for setup help
2. Review [AUDIT_REPORT.md](./AUDIT_REPORT.md) for technical details
3. Open an issue in the repository

---

## 🎉 Changelog

### Latest Update (2025-12-12)

**Added:**
- Google Sign-In authentication
- Google Drive cloud synchronization
- Multi-device access support
- User profile display
- Sync status indicator
- Auto-load latest invoice

**Fixed:**
- Missing attachment event listener
- XSS vulnerabilities with HTML escaping
- Negative number validation

**Security:**
- Added input sanitization
- Improved error handling
- Secure token storage

---

**Built with ❤️ for OAK Builders LLC**
