# MONA Pay for VS Code

A VS Code extension for developers integrating MONA Pay: log in, create a VietQR code, view the 20 most recent transactions of a virtual account, start a local webhook listener and insert webhook receiver snippets.

## Install

The extension is built from source and installed as a VSIX package. It needs Node.js 18+, VS Code 1.85+ and, for the webhook listener, the `monapay` CLI (`@monapay/cli`).

```bash
git clone https://github.com/mona-software/vscode-monapay.git
cd vscode-monapay
npm install
npm run compile
npx @vscode/vsce package
code --install-extension monapay-vscode-0.1.0.vsix
```

## Quick start

1. Open the Command Palette and run `MONA Pay: Đăng nhập` (Log in).
2. Enter your MONA Pay username, password and, for write actions such as creating a QR code, your client secret.
3. Run `MONA Pay: Xem giao dịch` (View transactions) and enter a virtual account number. The transactions appear in the MONA Pay view in the activity bar.

## Usage

### Commands

| Command | What it does |
| --- | --- |
| `MONA Pay: Đăng nhập` (Log in) | Checks the credentials against the API, then stores the password and client secret in VS Code Secret Storage |
| `MONA Pay: Tạo QR` (Create QR) | Asks for the ACB merchant details, order ID and amount, creates a dynamic VietQR through `@monapay/node`, copies `qr_data_url` to the clipboard and writes it to the `MONA Pay` output channel. Requires a client secret |
| `MONA Pay: Xem giao dịch` (View transactions) | Loads the 20 most recent transactions of a virtual account into the tree view |
| `MONA Pay: Nghe webhook local` (Listen for webhooks locally) | Opens a terminal and runs `monapay webhook listen --port 3939` |

### Snippets

Three snippets are available: `monapay-webhook-php`, `monapay-webhook-node` (JavaScript and TypeScript) and `monapay-webhook-python`. Each checks the timestamp within 300 seconds, verifies HMAC-SHA256 over the raw body and deduplicates by `transaction_code`.

## Configuration

| Setting | Default | Meaning |
| --- | --- | --- |
| `monapay.baseUrl` | `https://api.monapay.vn` | MONA Pay API base URL |
| `monapay.webhookPort` | `3939` | Port passed to `monapay webhook listen` |

Credentials are kept only in VS Code Secret Storage (password, client secret) and global state (username, last virtual account).

## Development

```bash
npm install
npm run compile   # or: npm run check (type-check only)
```

Press `F5` in VS Code to open an Extension Development Host.

The activity bar icon `media/icon-placeholder.svg` is a neutral placeholder, not the MONA Pay logo.

Documentation: https://monapay.vn/docs

## License

MIT

**MONA Pay is part of MONA Cloud by The MONA Group.**
