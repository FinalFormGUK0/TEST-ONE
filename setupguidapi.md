# Complete Setup Guide - API Keys & Configuration

This guide provides detailed step-by-step instructions to set up all required API keys, tokens, and configurations for the GitHub Actions RDP Automation System.

## 📋 Prerequisites Checklist

Before starting, ensure you have:
- [ ] A GitHub account with repository access
- [ ] A Gmail account
- [ ] A Telegram account
- [ ] A Tailscale account
- [ ] Admin access to your GitHub repository

## 🔑 Required Secrets Overview

You will need to configure these 8 secrets in GitHub:

| Secret Name | Source | Purpose |
|-------------|--------|---------|
| `PAT_TOKEN` | GitHub | Workflow permissions |
| `TELEGRAM_BOT_TOKEN` | Telegram BotFather | Bot communication |
| `TELEGRAM_CHAT_ID` | Telegram | Your chat ID |
| `EMAIL_SMTP_USER` | Gmail | SMTP username |
| `EMAIL_SMTP_PASS` | Gmail | App password |
| `EMAIL_FROM` | Gmail | Sender address |
| `EMAIL_TO` | Gmail/Other | Recipient address |
| `TAILSCALE_AUTH_KEY` | Tailscale | VPN authentication |

---

## 🐙 GitHub Setup

### Step 1: Create Personal Access Token (PAT)

1. **Navigate to GitHub Settings**
   - Go to [GitHub Settings](https://github.com/settings/tokens)
   - Click your profile picture → Settings
   - Scroll down to "Developer settings" in left sidebar

2. **Create New Token**
   - Click "Personal access tokens" → "Tokens (classic)"
   - Click "Generate new token" → "Generate new token (classic)"

3. **Configure Token Settings**
   ```
   Note: RDP Automation System
   Expiration: Custom (set to 1 year for convenience)
   ```

4. **Select Required Scopes**
   Check these permissions:
   - [ ] `repo` (Full control of private repositories)
   - [ ] `workflow` (Update GitHub Action workflows)
   - [ ] `actions` (Access to GitHub Actions)

5. **Generate and Copy Token**
   - Click "Generate token"
   - **IMPORTANT**: Copy the token immediately (starts with `ghp_`)
   - Example format: `ghp_1234567890abcdefghijklmnop`

### Step 2: Add GitHub Repository Secrets

1. **Navigate to Repository Settings**
   - Go to your repository
   - Click "Settings" tab
   - Click "Secrets and variables" → "Actions"

2. **Add PAT_TOKEN Secret**
   - Click "New repository secret"
   - Name: `PAT_TOKEN`
   - Secret: Paste your GitHub token
   - Click "Add secret"

---

## 📧 Gmail Setup

### Step 1: Enable 2-Factor Authentication

1. **Go to Google Account Security**
   - Visit [Google Account Security](https://myaccount.google.com/security)
   - Sign in to your Gmail account

2. **Enable 2-Step Verification**
   - Click "2-Step Verification"
   - Follow prompts to enable (phone number required)
   - Complete verification process

### Step 2: Generate App Password

1. **Access App Passwords**
   - Return to [Google Account Security](https://myaccount.google.com/security)
   - Click "2-Step Verification"
   - Scroll down to "App passwords"

2. **Create New App Password**
   - Click "App passwords"
   - Enter your password if prompted
   - App name: `RDP Automation`
   - Click "Generate"

3. **Copy App Password**
   - Copy the 16-character password (format: `xxxx xxxx xxxx xxxx`)
   - **IMPORTANT**: Save this password immediately

### Step 3: Add Gmail Secrets to GitHub

Add these 4 secrets to your GitHub repository:

1. **EMAIL_SMTP_USER**
   - Name: `EMAIL_SMTP_USER`
   - Secret: Your full Gmail address (e.g., `yourname@gmail.com`)

2. **EMAIL_SMTP_PASS**
   - Name: `EMAIL_SMTP_PASS`
   - Secret: The 16-character app password from Step 2

3. **EMAIL_FROM**
   - Name: `EMAIL_FROM`
   - Secret: Your Gmail address (same as SMTP_USER)

4. **EMAIL_TO**
   - Name: `EMAIL_TO`
   - Secret: Recipient email address (can be same or different)

---

## 🤖 Telegram Setup

### Step 1: Create Telegram Bot

1. **Start Chat with BotFather**
   - Open Telegram app/web
   - Search for `@BotFather`
   - Click "Start" or send `/start`

2. **Create New Bot**
   ```
   Send: /newbot
   BotFather: Alright, a new bot. How are we going to call it?
   You: RDP Controller Bot
   
   BotFather: Good. Now let's choose a username for your bot.
   You: your_rdp_controller_bot
   ```

3. **Save Bot Token**
   - BotFather will provide a token like: `123456789:ABCdefGHIjklMNOpqrsTUVwxyz`
   - **IMPORTANT**: Copy and save this token

### Step 2: Get Your Chat ID

#### Method 1: Using Bot Commands (Recommended)

1. **Start Chat with Your Bot**
   - Search for your bot by username
   - Click "Start" or send any message

2. **Get Updates via API**
   - Open browser and visit (replace `YOUR_BOT_TOKEN`):
   ```
   https://api.telegram.org/botYOUR_BOT_TOKEN/getUpdates
   ```
   - Example:
   ```
   https://api.telegram.org/bot123456789:ABCdefGHIjklMNOpqrsTUVwxyz/getUpdates
   ```

3. **Find Your Chat ID**
   - Look for `\"chat\":{\"id\":123456789` in the response
   - Your chat ID is the number after `\"id\":`
   - Example: `123456789` or `-123456789`

#### Method 2: Using @userinfobot

1. Search for `@userinfobot` in Telegram
2. Start chat and send `/start`
3. Bot replies with your user information including Chat ID

### Step 3: Add Telegram Secrets to GitHub

1. **TELEGRAM_BOT_TOKEN**
   - Name: `TELEGRAM_BOT_TOKEN`
   - Secret: Your bot token from Step 1

2. **TELEGRAM_CHAT_ID**
   - Name: `TELEGRAM_CHAT_ID`
   - Secret: Your chat ID from Step 2

---

## 🌐 Tailscale Setup

### Step 1: Create Tailscale Account

1. **Sign Up for Tailscale**
   - Visit [Tailscale](https://tailscale.com/)
   - Click "Get started for free"
   - Sign up with Google, Microsoft, or GitHub

2. **Verify Email**
   - Check your email for verification
   - Click verification link

### Step 2: Generate Auth Key

1. **Access Admin Console**
   - Go to [Tailscale Admin Console](https://login.tailscale.com/admin/settings/keys)
   - Sign in to your account

2. **Create Auth Key**
   - Click "Generate auth key"
   - Configure settings:
     ```
     Description: GitHub Actions RDP
     Expires: 90 days (or longer)
     Reusable: Yes (recommended)
     Ephemeral: No
     Tags: (leave empty)
     ```

3. **Generate and Copy Key**
   - Click "Generate key"
   - Copy the key (starts with `tskey-auth-`)
   - Example: `tskey-auth-1234567890abcdef`

### Step 3: Add Tailscale Secret to GitHub

1. **TAILSCALE_AUTH_KEY**
   - Name: `TAILSCALE_AUTH_KEY`
   - Secret: Your auth key from Step 2

---

## ✅ Verification Checklist

After completing all steps, verify you have these 8 secrets in GitHub:

- [ ] `PAT_TOKEN` - GitHub personal access token
- [ ] `TELEGRAM_BOT_TOKEN` - Telegram bot token  
- [ ] `TELEGRAM_CHAT_ID` - Your Telegram chat ID
- [ ] `EMAIL_SMTP_USER` - Gmail address
- [ ] `EMAIL_SMTP_PASS` - Gmail app password
- [ ] `EMAIL_FROM` - Sender email address
- [ ] `EMAIL_TO` - Recipient email address
- [ ] `TAILSCALE_AUTH_KEY` - Tailscale authentication key

### GitHub Secrets Verification

1. **Check Repository Secrets**
   - Go to Repository → Settings → Secrets and variables → Actions
   - Verify all 8 secrets are listed
   - Names must match exactly (case-sensitive)

2. **Test Secret Access**
   - Secrets should show "Updated X time ago"
   - Cannot view secret values (this is normal)

---

## 🧪 Testing Your Setup

### Test 1: Telegram Bot

1. **Send Test Message**
   - Open your bot chat
   - Send: `Hello bot!`

2. **Verify API Response**
   - Visit: `https://api.telegram.org/botYOUR_BOT_TOKEN/getUpdates`
   - Should see your test message in JSON response

### Test 2: Gmail SMTP

1. **Test Email Sending** (Optional)
   - Use an email client or tool to test SMTP
   - Server: `smtp.gmail.com`
   - Port: `587` (TLS) or `465` (SSL)
   - Username: Your Gmail address
   - Password: App password

### Test 3: Tailscale Auth

1. **Verify Auth Key**
   - Check Tailscale admin console
   - Auth key should be listed and active
   - Not yet used by any devices

### Test 4: GitHub Actions

1. **Run Test Workflow**
   - Manually trigger `Start_whole_WorkFlow.yml`
   - Check logs for secret access errors
   - Should not show "secret not found" errors

---

## 🚨 Security Best Practices

### Do's ✅
- Store all secrets securely in GitHub Secrets
- Use unique app passwords for Gmail
- Set reasonable expiration dates for tokens
- Regularly rotate auth keys and tokens
- Use descriptive names for API keys

### Don'ts ❌
- Never commit secrets to code repositories
- Don't share bot tokens or auth keys
- Don't use your main Gmail password
- Don't set tokens to never expire
- Don't use weak or predictable chat IDs

### Emergency Procedures 🆘

**If secrets are compromised:**

1. **GitHub PAT**: Revoke and regenerate in GitHub settings
2. **Telegram Bot**: Contact @BotFather, revoke token, create new bot
3. **Gmail**: Revoke app password, generate new one
4. **Tailscale**: Delete auth key, generate new one

---

## 🛠️ Troubleshooting

### Common Issues

#### GitHub Secrets
- **Issue**: "Secret not found" in workflow logs
- **Solution**: Check secret name spelling (case-sensitive)

#### Telegram Bot
- **Issue**: Bot doesn't respond to messages
- **Solution**: Ensure you've sent at least one message to activate chat

#### Gmail SMTP
- **Issue**: Authentication failed
- **Solution**: Verify 2FA is enabled and app password is correct

#### Tailscale
- **Issue**: Auth key rejected
- **Solution**: Check key hasn't expired and is marked as reusable

### Debug Commands

#### Test Telegram API
```bash
curl "https://api.telegram.org/botYOUR_BOT_TOKEN/getMe"
```

#### Test GitHub API
```bash
curl -H "Authorization: token YOUR_PAT_TOKEN" https://api.github.com/user
```

---

## 📞 Support Resources

### Official Documentation
- [GitHub Personal Access Tokens](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)
- [Gmail App Passwords](https://support.google.com/accounts/answer/185833)
- [Telegram Bot API](https://core.telegram.org/bots/api)
- [Tailscale Auth Keys](https://tailscale.com/kb/1085/auth-keys/)

### Community Support
- [GitHub Actions Community](https://github.community/)
- [Telegram Bot Developers](https://t.me/BotSupport)
- [Tailscale Community](https://tailscale.com/community/)

---

**Setup Complete!** 🎉

Once all secrets are configured, your RDP automation system is ready to use. Run the `Start_whole_WorkFlow.yml` workflow to begin monitoring for Telegram commands.

**Last Updated**: 2025-09-14  
**Version**: 1.0  
**Estimated Setup Time**: 30-45 minutes