# Welcome-Canvas

Welcome-Canvas is a Node.js module for creating customized welcome images for Discord servers. It allows you to generate beautiful welcome images with user avatars, usernames, and a custom message.

## Installation

You can install Welcome-Canvas via npm:

```bash
npm install welcome-canvas
```

## Usage

Here's an example of how to use Welcome-Canvas in your Discord bot:

```javascript
const { Client, GatewayIntentBits } = require('discord.js');
const { welcome } = require('welcome-canvas'); 

const client = new Client({
  intents: [
    GatewayIntentBits.Guilds,
    GatewayIntentBits.GuildMembers,
  ],
});

// Define an array of background images
const backgroundImages = [
    'https://s6.imgcdn.dev/ZpcLw.png',
    'https://s6.imgcdn.dev/ZpCUT.png',
    'https://s6.imgcdn.dev/Zp4wt.png',
    'https://s6.imgcdn.dev/ZpNo9.png',
    'https://s6.imgcdn.dev/Zpisy.png',
    'https://s6.imgcdn.dev/Zpkx8.png',
    'https://s6.imgcdn.dev/ZpnH2.png',
  ];

let currentBackgroundIndex = 0; 

client.on('ready', () => {
  console.log(`Logged in as ${client.user.tag}`);
});

client.on('guildMemberAdd', async (member) => {
  const channelId = '1157243263728762900'; // Replace with the desired channel ID
  const channel = await client.channels.fetch(channelId); // Fetch the channel by ID
  if (channel) {
   
    const welcomeCard = new welcome()
      .setName(member.user.username)
      .setAvatar(member.user.displayAvatarURL({ format: 'png' }))
      .setTitle('Welcome')
      .setMessage(`You are our ${member.guild.memberCount} Member`)
      .setBackground(backgroundImages[currentBackgroundIndex]); // Use the current background

    
    const welcomeImageBuffer = await welcomeCard.build();

    
    channel.send({ files: [welcomeImageBuffer] });

    
    currentBackgroundIndex = (currentBackgroundIndex + 1) % backgroundImages.length;
  }
});


client.login('YOUR_BOT_TOKEN');
```

## API

### new welcome(options)
- `options` (Object) - An object with the following optional properties:
  - `username` (String) - The username to display on the welcome card.
  - `avatar` (String) - The URL of the user's avatar.
  - `title` (String) - The title text on the welcome card.
  - `message` (String) - The message to display on the welcome card.
  - `background` (String) - The background to display on the welcome card.
### setName(name)
- Set the username for the welcome card.

### setAvatar(image)
- Set the avatar image for the welcome card.

### setTitle(title)
- Set the title text for the welcome card.

### setColor(color)
- Set the color for text and graphics on the welcome card.

### setMessage(message)
- Set the message to display on the welcome card.

### setbackground(background)
- Set the background to display on the welcome card.


## Preview
![preview](https://s6.imgcdn.dev/9Dw5M.png)

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

This module is based on napi-rs/canvas for canvas rendering.

## Contact

If you have any questions or suggestions, feel free to [contact us](https://discord.gg/cool-music-support-925619107460698202).
