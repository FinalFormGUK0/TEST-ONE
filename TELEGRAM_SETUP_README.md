# Telegram Bot Setup Guide for RDP Control

This guide provides step-by-step instructions to set up a Telegram bot that can receive "Stop_rdp" commands to control your GitHub Actions RDP workflows.

## 📋 Prerequisites

- A Telegram account
- Access to your GitHub repository settings
- Basic understanding of Telegram bots

## 🤖 Step 1: Create a Telegram Bot

### 1.1 Start a chat with BotFather
1. Open Telegram app or web version
2. Search for `@BotFather` (official bot creation bot)
3. Start a conversation by clicking "Start" or typing `/start`

### 1.2 Create your bot
1. Send command: `/newbot`
2. BotFather will ask for a bot name (display name) - example: `RDP Controller`
3. BotFather will ask for a username (must end with 'bot') - example: `your_rdp_controller_bot`
4. **IMPORTANT**: Save the bot token that BotFather provides - it looks like:
   ```
   123456789:ABCdefGHIjklMNOpqrsTUVwxyz
   ```

### 1.3 Configure your bot (Optional but recommended)
```
/setdescription - Set a description for your bot
/setabouttext - Set an about text
/setuserpic - Set a profile picture
```

## 🔍 Step 2: Get Your Chat ID

### Method 1: Using Bot Commands (Recommended)
1. Search for your newly created bot in Telegram
2. Start a chat with your bot
3. Send any message to your bot (like "Hello")
4. Open this URL in your browser (replace `YOUR_BOT_TOKEN` with your actual token):
   ```
   https://api.telegram.org/botYOUR_BOT_TOKEN/getUpdates
   ```
5. Look for the `"chat"` object in the JSON response and find the `"id"` field
6. **IMPORTANT**: Save this Chat ID - it will be a number like `123456789` or `-123456789`

### Method 2: Using @userinfobot
1. Search for `@userinfobot` in Telegram
2. Start a chat and send `/start`
3. The bot will reply with your user information including your Chat ID

### Method 3: Using @chatidbot
1. Search for `@chatidbot` in Telegram  
2. Start a chat and send `/start`
3. The bot will reply with your Chat ID

## ⚙️ Step 3: Configure GitHub Secrets

### 3.1 Navigate to Repository Settings
1. Go to your GitHub repository
2. Click on **Settings** tab
3. In the left sidebar, click **Secrets and variables** → **Actions**

### 3.2 Add Required Secrets
Click **New repository secret** for each of the following:

#### Secret 1: TELEGRAM_BOT_TOKEN
- **Name**: `TELEGRAM_BOT_TOKEN`
- **Value**: Your bot token from Step 1.2 (e.g., `123456789:ABCdefGHIjklMNOpqrsTUVwxyz`)

#### Secret 2: TELEGRAM_CHAT_ID  
- **Name**: `TELEGRAM_CHAT_ID`
- **Value**: Your chat ID from Step 2 (e.g., `123456789`)

### 3.3 Verify Secrets
After adding both secrets, you should see:
- ✅ `TELEGRAM_BOT_TOKEN`
- ✅ `TELEGRAM_CHAT_ID`

## 🧪 Step 4: Test Your Setup

### 4.1 Test Bot Communication
1. Send a message to your bot: `Hello bot!`
2. Use the getUpdates URL again to verify the message appears:
   ```
   https://api.telegram.org/botYOUR_BOT_TOKEN/getUpdates
   ```

### 4.2 Test with GitHub Actions
1. Run your `Stand_by.yml` workflow manually
2. Check the workflow logs to ensure no Telegram errors appear
3. The workflow should show: `🔍 Starting 6-hour standby monitoring for 'Stop_rdp' command`

## 🎮 Step 5: Using the Bot

### How to Stop RDP
1. When your RDP workflows are running
2. Send this exact message to your bot: `Stop_rdp`
3. The Stand_by workflow will:
   - Detect the command within 10 minutes
   - Cancel the running RDP email workflow
   - Send you an email confirmation
   - Exit without rerunning the cycle

### Important Notes
- ⚠️ The command is case-sensitive: use `Stop_rdp` exactly
- ⏱️ The bot checks for messages every 10 minutes
- 📧 You'll receive email notifications for cancellation status
- 🔄 If no stop command is received in 6 hours, the cycle continues

## 🛠️ Troubleshooting

### Common Issues

#### Issue 1: "Telegram credentials not configured"
**Solution**: Verify both `TELEGRAM_BOT_TOKEN` and `TELEGRAM_CHAT_ID` secrets are set correctly

#### Issue 2: Bot doesn't respond to commands
**Solutions**:
- Ensure you've started a chat with your bot first
- Verify the bot token is correct
- Check that the chat ID corresponds to your conversation with the bot

#### Issue 3: Wrong Chat ID
**Symptoms**: Bot logs show messages but doesn't detect your commands
**Solution**: 
- Make sure you're using the Chat ID from YOUR conversation with the bot
- If using a group chat, the Chat ID will be negative (e.g., `-123456789`)

#### Issue 4: getUpdates shows empty results
**Solutions**:
- Make sure you've sent at least one message to your bot
- Try refreshing the URL after sending a new message
- Verify the bot token in the URL is correct

## 🔒 Security Best Practices

1. **Keep Your Bot Token Secret**: Never share it publicly or commit it to code
2. **Limit Bot Permissions**: Your bot only needs to receive messages
3. **Use Private Chats**: Don't add the bot to public groups unnecessarily
4. **Regular Token Rotation**: Consider regenerating bot tokens periodically using BotFather's `/revoke` command

## 📚 Additional Resources

- [Telegram Bot API Documentation](https://core.telegram.org/bots/api)
- [BotFather Commands Reference](https://core.telegram.org/bots#6-botfather)
- [GitHub Actions Secrets Documentation](https://docs.github.com/en/actions/security-guides/encrypted-secrets)

## ❓ Support

If you encounter issues:
1. Check the GitHub Actions logs for specific error messages
2. Verify all secrets are correctly configured
3. Test the Telegram bot independently using the getUpdates URL
4. Ensure your bot has been started (sent at least one message)

---
**Last Updated**: Created for RDP Control System
**Version**: 1.0