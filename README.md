# Beginner Chatbot Development
A guide to creating chatbots and conversational interfaces

## Prerequisites

* [node.js](https://github.com/nodejs/node/wiki/Installation)

* ngrok

    >ngrok creates a secure public URL to a local webserver on your machine. Iterate quickly with immediate feedback without interrupting flow.
    
    ```bash
    npm install -g ngrok
    
    ```
    If your package manager of choice is Homebrew, install via `brew cask install ngrok`

    If it's your first time globally downloading a package using Node OR you're getting EACCES/permission denied you will need to update your permissions: 

    https://docs.npmjs.com/getting-started/fixing-npm-permissions



## Getting started

### Clone this repo and migrate to the directory
```bash
git clone https://github.com/devcfacebook/oakbot-intro
cd oakbot-intro
```

### Set up your environment variables

* Create a `.env` file within the directory
* Copy the contents from the `.env.example` into the `.env` file

These variables are necessary to have a functioning server. We will update the values later

### Install npm modules to local file

```bash
npm install
```

### Start up your app server

```bash
npm start
```

In the browser, navigate to the webhook route on your [localhost](http://localhost:5000/webhook)

*At this point, your browser should show a 'Forbidden' status and your server should output an error message stating: 'Failed validation. Validation token mismatch'*


### Start up the ngrok server within another terminal 

```bash
ngrok http 5000
```

In the browser, navigate to your webhook route on the public url provided to you by ngrok in your Terminal, e.g. <https://99fca400.ngrok.io/webhook>

Confirm that you receive the same status and log message as earlier

Now let's deploy our bot so we can start interacting with it!

# Messenger Platform for Bots 

To build a bot on the Messenger platform, the following items are necessary:

> Facebook Page: A Facebook Page will be used as the identity of your bot. When people chat with your app, they will see the Page name and the Page profile picture

> Facebook Developer Account: Your developer account is required to create new apps, which are the core of any Facebook integration

> Facebook App: The Facebook app contains the settings for your Messenger bot, including access tokens

> Webhook URL: Actions that take place in conversations with your bot, such as new messages are sent as events to your webhook

## Create a FB page

<https://www.facebook.com/pages/create>

## Create a FB developer account and a FB app

<https://developers.facebook.com/apps/>

## Add messenger capabilities to FB app

 Go to the App Dashboard and under Product Settings on the bottom left corner, click "Add Product" and select "Messenger"

 ![](https://scontent-mia3-2.xx.fbcdn.net/v/t39.2178-6/12995587_195576307494663_824949235_n.png?oh=2c4beb8b65bbe674b9d02e55baded4fb&oe=5A7C24C3)

## Connect FB app with bot server

* Within your file directory, update the VALIDATION_TOKEN in the .env file to any value you desire 

* On the Messenger page, browse to the Webhooks section, and select "Setup Webhooks"

![](https://scontent-mia3-2.xx.fbcdn.net/v/t39.2178-6/13331609_660771177408445_306127577_n.png?oh=b2c73c9b6a96d514e26b312d507df043&oe=5A87674C)

* Enter your ngrok url, with the `/webhook` route added (e.g. <https://99fca400.ngrok.io/webhook>) into the callback url field

* Enter the value of your VALIDATION_TOKEN into the verify token field

* Within the subscription fields section, select the messages and messaging_postbacks option

![](https://scontent-mia3-2.xx.fbcdn.net/v/t39.2178-6/12057143_211110782612505_894181129_n.png?oh=566821dc645b301f1356be2c1c7c35ef&oe=5A78B2F1)

* Troubleshooting: Restart `npm start` and `ngrok http 5000`. Note: This will change your ngrok URL

## Collect App Secret

* On the left hand side, go to `Settings`, browse to the `App Secret` section and click on `Show`
* Copy the `App Secret` and use it to set the `APP_SECRET` variable within your `.env` file


## Collect page access token

* On the left hand side, go to `Messenger`, browse to the `Token Generation` section and select your page
* Copy the generated `Page Access Token` and use as the value for the `PAGE_ACCESS_TOKEN` variable in your `.env` file

![](https://scontent-mia3-2.xx.fbcdn.net/v/t39.2178-6/12995543_1164810200226522_2093336718_n.png?oh=27f1f08c8e2ee6139f1a93d24d92aece&oe=5A476D09)
	 
## Link messenger app to page

Browse to the Webhooks section and select your page to forward the messaging and postback events to your the webhook route. Click `Subscribe`

![enter image description here](https://scontent-mia3-2.xx.fbcdn.net/v/t39.2178-6/13421551_1702530599996541_471321650_n.png?oh=60b2566071cfb9662ce3c303d3ab3d8e&oe=5A4E859F)


# Wrapping it up 

Restart your bot server (the terminal running `npm start`) to begin receiving content from your FB messenger app. Do not restart ngrok as this will change your URL!

Send a message as a visitor to your FB page and watch the message be echoed back to you. 

Follow these steps to quickly access your bot through Facebook:

1) Navigate to your Facebook Page and click the 'add a username' under the profile picture.

2) Add a username, preferrably the same name of your Bot

3) You should now be given a link to your Bot. Navigate to that link, and send a message to your bot. 


# Deploying Your Bot

1) Navigate to the [following tutorial](https://devcenter.heroku.com/articles/getting-started-with-nodejs#introduction) to deploy your Bot Server to Heroku.

2) Once you go through those steps, make sure to do the following APP_SECRET, PAGE_TOKEN, AND VALIDATION_TOKEN to your [config variables](https://devcenter.heroku.com/articles/config-vars).

3) You stopped running your instance of ngrok so that heroku can use the port


4) Navigate to the Messenger Platform in your Browser and scroll down to WebHooks. Click on 'edit subscription' and update your WebHook link to point to your Heroku link + /webhook
