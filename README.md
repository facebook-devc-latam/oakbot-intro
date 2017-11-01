# Beginner Chabot Development
A guide to creating chatbots and conversational interfaces

## Prerequisites

* [node.js](https://github.com/nodejs/node/wiki/Installation)

* ngrok

    >ngrok creates a secure public URL to a local webserver on your machine. Iterate quickly with immediate feedback without interrupting flow.
    
    ```bash
    npm install -g ngrok
    ```
    If your package manager of choice is Homebrew, install via `brew install ngrok`

## Installation

Clone this repo and install dependencies
```bash
git clone
cd oak-bot
npm install
```

## Getting started

Start up your bot server
```bash
npm start
```

Within another terminal tab or window, start up the ngrok server
```bash
ngrok http 5000
```

# Messenger Platform 