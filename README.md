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

## Using Keyman (uvx)

A convenient option is to use `uvx` to run the tool, without installing it:

```bash
# Set up the tool
uvx am-keyman configure TEAM_ID_HERE KEY_ID_HERE KEY_FILE_PATH
# Run the entire flow (dev token, user token)
uvx am-keyman get-tokens
```

## Using Keyman (pip)

The CLI utility is published on PyPA:

```bash
pip install am-keyman
am-keyman
```

## Using Keyman (local development)

```bash
uv sync
uv build
# Set up the tool
uv run am-keyman configure TEAM_ID_HERE KEY_ID_HERE KEY_FILE_PATH
# Run the entire flow (dev token, user token)
uv run am-keyman get-tokens
# OPTIONAL: Get your developer token 
uv run am-keyman get-dev-token 
# OPTIONAL: Grab a user token for yourself
uv run am-keyman get-user-token DEV_TOKEN_HERE
# ... a web server will open up, follow the instructions
# ... after completion, the token will show up in the console
```

## Important note

If you mean to grab a user token using the command-line utility, **do not use Firefox**.

The stricter security settings built into the browser will break the OAuth flow and it won't work.

Safari worked great for me.
