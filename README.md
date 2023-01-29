This is a fork of OpenAI's GPT-3 Discord Bot that has been modified to have unlimited memory. I utilized David Shapiro's code with some modifications to achieve this, all credit for this goes to David and others who have done this before me. His code is available here: https://github.com/daveshap/LongtermChatExternalSources
Currently the bot only remembers what you tell it, not what it tells you, I just haven't had time to implement this yet.

In addition to long term memory the bot has been brought out from threads and will talk in regular text channels and does not need / commands. The bot will talk in every channel that it has permission to talk in, including threads, so be mindful of where you put your bot and what permissions it has. All permissions can be modified inside the Discord app. Also, all moderation has been turned off and removed from the code, be careful.

Example Discord bot written in Python that uses the [completions API](https://beta.openai.com/docs/api-reference/completions) to have conversations with the `text-davinci-003` model, and the [moderations API](https://beta.openai.com/docs/api-reference/moderations) to filter the messages.

This bot uses the [OpenAI Python Library](https://github.com/openai/openai-python) and [discord.py](https://discordpy.readthedocs.io/).

# Features

- The model will generate a reply for every user message in any thread or text channel it has access to
- The past 5 messages and any history relating to the topic will be passed to GPT-3 with every message
- you can customize the bot instructions by modifying `config.yaml`
- you can change the model, the hardcoded value is `text-davinci-003`, the bot also uses 'embeddings-ada-002' for saving its memory

# Setup

1. Copy `.env.example` to `.env` and start filling in the values as detailed below (make sure .env is .env and not .env.txt)
1. Go to https://beta.openai.com/account/api-keys, create a new API key, and fill in `OPENAI_API_KEY`
1. Create your own Discord application at https://discord.com/developers/applications
1. Go to the Bot tab and click "Add Bot"
    - Click "Reset Token" and fill in `DISCORD_BOT_TOKEN`
    - Disable "Public Bot" unless you want your bot to be visible to everyone
    - Enable "Message Content Intent" under "Privileged Gateway Intents"
1. Go to the OAuth2 tab, copy your "Client ID", and fill in `DISCORD_CLIENT_ID`
1. Copy the ID the server you want to allow your bot to be used in by right clicking the server icon and clicking "Copy ID". Fill in `ALLOWED_SERVER_IDS`. If you want to allow multiple servers, separate the IDs by "," like `server_id_1,server_id_2`
2. Create folders inside the src directory for each of the following: chat_logs , memories , notes (I need to add this into the code but just haven't gotten to it.)
3. Install dependencies and run the bot
    ```
    pip install -r requirements.txt
    python -m src.main
    ```
    You should see an invite URL in the console. Copy and paste it into your browser to add the bot to your server.

# FAQ

> Why isn't my bot responding to commands?

Ensure that the channels your bots have access to allow the bot to have these permissions.
- Send Messages
- Send Messages in Threads
- Create Public Threads
- Manage Messages (only for moderation to delete blocked messages)
- Manage Threads
- Read Message History
- Use Application Commands
