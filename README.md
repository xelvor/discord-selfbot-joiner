

# Discord Selfbot Joiner

[![npm version](https://badge.fury.io/js/discord-selfbot-joiner.svg)](https://www.npmjs.com/package/discord-selfbot-joiner)
[![GitHub issues](https://img.shields.io/github/issues/xelvor/discord-selfbot-joiner)](https://github.com/xelvor/discord-selfbot-joiner/issues)
[![MIT license](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/xelvor/discord-selfbot-joiner/blob/main/LICENSE)
[![Downloads](https://img.shields.io/npm/d18m/discord-selfbot-joiner.svg)](https://www.npmjs.com/package/discord-selfbot-joiner)

A Node.js package for allowing a Discord selfbot to join servers by bypassing CAPTCHA with OAuth2 authentication. This package uses [discord.js-selfbot-v13](https://www.npmjs.com/package/discord.js-selfbot-v13) and `axios` for making API requests.

## Features

- Bypasses CAPTCHA for Discord server join requests
- OAuth2 authentication for Discord bots
- Simple and customizable configuration

## Installation

To install the package, use npm:

```bash
npm install discord-selfbot-joiner
```

## Usage

Here's an example of how to use the package to add a Discord selfbot to a guild:

```typescript
import { Client } from 'discord.js-selfbot-v13';
import { authorizeBot } from 'discord-selfbot-joiner';

const client = new Client();

const botConfig = {
    clientId: 'your-client-id',
    clientSecret: 'your-client-secret',
    redirectUri: 'http://localhost:3000/oAuth',
    apiEndpoint: 'https://discord.com/api/v10',
    guildId: 'your-guild-id',
    botToken: 'your-bot-token'
};

client.on('ready', async () => {
    console.log('Bot is ready!');
    
    const authURL = `https://discord.com/oauth2/authorize?client_id=${botConfig.clientId}&response_type=code&redirect_uri=${encodeURIComponent(botConfig.redirectUri)}&scope=guilds.join+identify`;

    const response = await authorizeBot(client, authURL, botConfig);
    console.log(response);
});

client.login(botConfig.botToken);
```

### Configuration

You can dynamically pass your configuration using the following object structure:

```typescript
const botConfig = {
    clientId: 'your-client-id',
    clientSecret: 'your-client-secret',
    redirectUri: 'http://localhost:3000/oAuth',
    apiEndpoint: 'https://discord.com/api/v10',
    guildId: 'your-guild-id',
    botToken: 'your-bot-token'
};
```

### Functions

- `authorizeBot(client: Client, authURL: string, config: OAuthConfig)`: This function authorizes the bot and handles the OAuth2 flow to add a user to a guild.
- `oAuth(code: string, config: OAuthConfig)`: Manages the OAuth2 authentication and token exchange.

## Example Authorization URL

The OAuth2 URL for authorizing the bot:

```
https://discord.com/oauth2/authorize?client_id=YOUR_CLIENT_ID&response_type=code&redirect_uri=http://localhost:3000/oAuth&scope=guilds.join+identify
```

Replace `YOUR_CLIENT_ID` with your actual client ID and ensure the `redirect_uri` matches the one set in your Discord developer application.

## Contributing

If you'd like to contribute, please feel free to submit a pull request or open an issue in the [GitHub repository](https://github.com/xelvor/discord-selfbot-joiner/issues).

## License

This project is licensed under the MIT License. See the [LICENSE](https://github.com/xelvor/discord-selfbot-joiner/blob/main/LICENSE) file for details.

## Links

- [GitHub Repository](https://github.com/xelvor/discord-selfbot-joiner)
- [NPM Package](https://www.npmjs.com/package/discord-selfbot-joiner)

---

### Badges
- **npm version badge**: Links to your npm page and shows the latest version.
- **GitHub issues badge**: Shows the number of open issues.
- **License badge**: Indicates that your project is MIT licensed.
