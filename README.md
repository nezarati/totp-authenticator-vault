# TOTP-Authenticator-Vault
Offline-ready TOTP authenticator with encrypted backups (AES-GCM), QR scanning, SHA1/SHA256/SHA512 support, and a clean mobile interface. Import/export .2fas files, copy codes with countdown ring, and manage 2FA tokens securely. No server, no tracking.
# TOTP Authenticator Vault

![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)
![Works offline](https://img.shields.io/badge/offline-ready-brightgreen)

## 🌐 Live Demo

Experience the app directly in your browser:

👉 **[TOTP Authenticator Vault - Live Demo](https://nezarati.github.io/TOTP-Authenticator-Vault/)**

This is a fully functional, client-side application. Your secrets and keys never leave your device.

## Features

- **Full Google Authenticator compatibility** – supports SHA1, SHA256, SHA512, 6/7/8 digits, 30/60s periods.
- **Encrypted backups** – export/import `.2fas` files with AES‑GCM + PBKDF2 (150k iterations).
- **QR code scanning** – add keys by scanning `otpauth://` QR codes directly from your camera.
- **Hide/Show OTP codes** – tap any 6‑digit code to blur it for privacy.
- **Countdown ring inside copy button** – visual progress and seconds left, with color warning at 5/10s.
- **Edit account names** – click on any name to rename.
- **Reveal secret key** – see the Base32 secret without auto‑copy (optional manual copy).
- **Works 100% offline** – no internet required after first load.
- **Mobile‑first design** – responsive, touch‑friendly, fits iPhone/Android perfectly.

## How to use

1. **Open the app** – just serve `index.html` or use the live demo (if hosted).
2. **Add a key** – paste a `otpauth://` URI or a Base32 secret, optionally set a custom account name.
3. **Scan a QR** – click the camera button and align the code.
4. **Manage** – copy codes with the button (ring shows remaining time), tap the code to hide/show, click the name to edit, delete with the red button.
5. **Back up** – export all keys with a strong password to a `.2fas` file. Import the same file to restore on any device.

## Security & Encryption

- All keys are stored **only in your browser’s memory** (no local storage unless you export).
- Exported files are encrypted using **AES‑GCM** with a password stretched via **PBKDF2 (150k iterations, SHA‑256)**.
- The default password (`2fas-default-encryption-key-2024`) is **weak** – use your own strong password for real security.
- The app never sends any data over the network – it’s a pure static web app.

## Installation (self‑host)

1. Download `index.html` from this repo.
2. Place it on any web server or open directly with your browser (`file://` protocol works).
3. For the best experience, serve over HTTPS (required for camera access in QR scanner).

## Supported URI parameters

The app respects the official `otpauth://totp/` specification:

| Parameter      | Supported values                          |
|----------------|-------------------------------------------|
| `secret`       | Base32 (required)                         |
| `algorithm`    | SHA1, SHA256, SHA512 (default SHA1)       |
| `digits`       | 6, 7, 8 (default 6)                       |
| `period`       | 30, 60 (default 30)                       |

Example:  
`otpauth://totp/Example:alice@google.com?secret=JBSWY3DPEHPK3PXP&algorithm=SHA256&digits=8&period=30`

## Development

This is a single‑file HTML/CSS/JS app. No build step, no dependencies except:
- [`jsQR`](https://github.com/cozmo/jsQR) for QR scanning (loaded via CDN).
- Web Crypto API (native).

To run locally:
```bash
git clone https://github.com/yourusername/totp-authenticator-vault.git
cd totp-authenticator-vault
# open index.html in your browser
