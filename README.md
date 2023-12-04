# Apple Music Keyman
A small utility that gets Apple Music API keys for you. It even allows getting *user tokens*, which are a bit more annoying since they involve a whole OAuth flow.

This tool is rudimentary and a work in progress.

## How Apple Music authorization works
You need a couple of things:

1. Apple Developer subscription. Yes, a paid one
2. A certificate generated with access to Apple Music & MusicKit APIs.
3. A Key ID for that certificate.
4. A Team ID for your developer account

Using the team ID, private key file (.p8) and key ID, you build a JWT that becomes your **developer token**. This token alone allows access to AM resources that aren't related to a user.

With that developer token, you can initiate an OAuth flow to get a **user token**. This one allows you to access the listening history for your account, for example.

## Using Keyman
```bash
poetry install
# Set up the tool
poetry run am-keyman configure TEAM_ID_HERE KEY_ID_HERE KEY_FILE_PATH
# Get your developer token 
poetry run am-keyman get-dev-token 
# OPTIONAL: Grab a user token for yourself
poetry run am-keyman get-user-token DEV_TOKEN_HERE
# ... a web server will open up, follow the instructions
# ... after completion, the token will show up in the console
```
