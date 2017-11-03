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

*Troubleshooting: If it's your first time globally downloading a package using Node OR you're getting EACCES/permission denied error you will need to update your [permissions](https://docs.npmjs.com/getting-started/fixing-npm-permissions)*



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

*At this point, your browser should show a* `Forbidden` *status and your server should output an error message stating:* `Failed validation. Validation token mismatch`


### Start up the ngrok server within another terminal

```bash
ngrok http 5000
```

In the browser, navigate to your webhook route on the public url provided to you by ngrok in your terminal, e.g. <https://99fca400.ngrok.io/webhook>

Confirm that you receive the same status and log message as earlier

Now let's connect our bot to the Facebook Messenger platform so we can start interacting with it!

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

 Go to the `App Dashboard` and under `Product Settings` on the bottom left corner, click `Add Product` and select `Messenger`

 ![](https://scontent-mia3-2.xx.fbcdn.net/v/t39.2178-6/12995587_195576307494663_824949235_n.png?oh=2c4beb8b65bbe674b9d02e55baded4fb&oe=5A7C24C3)

  ## Collect app secret

* On the left hand side, select `Settings`, browse to the `App Secret` section and click on `Show`

* Update the value of `APP_SECRET` variable within the `.env` file with your `App Secret`

## Collect page access token

* On the left hand side, go to `Messenger`, browse to the `Token Generation` section and select your page

* Update the value of the `PAGE_ACCESS_TOKEN` variable in your `.env` file with the generated `Page Access Token`

![](https://scontent-mia3-2.xx.fbcdn.net/v/t39.2178-6/12995543_1164810200226522_2093336718_n.png?oh=27f1f08c8e2ee6139f1a93d24d92aece&oe=5A476D09)

## Subscribe to user interactions

* Update the `VALIDATION_TOKEN` in the `.env` file to any value you desire 

* On the `Messenger` page, browse to the `Webhooks` section, and select `Setup Webhooks`

![](https://scontent-mia3-2.xx.fbcdn.net/v/t39.2178-6/13331609_660771177408445_306127577_n.png?oh=b2c73c9b6a96d514e26b312d507df043&oe=5A87674C)

* Enter your ngrok url, with the `/webhook` route added (e.g. <https://99fca400.ngrok.io/webhook>) into the callback url field

* Enter the value of your `VALIDATION_TOKEN` into the verify token field

* Within the subscription fields section, select the `messages` and `messaging_postbacks` options

![](https://scontent-mia3-2.xx.fbcdn.net/v/t39.2178-6/12057143_211110782612505_894181129_n.png?oh=566821dc645b301f1356be2c1c7c35ef&oe=5A78B2F1)

*Troubleshooting: If you are having difficulty with webhook setup, try restarting `npm start` and `ngrok http 5000`. Note: This will change your ngrok url so update the webhook callback url field with the new ngrok url and the `/webhook` route*

* Select your page to forward the messaging and postback events to your webhook route. Click `Subscribe`

![](https://scontent-mia3-2.xx.fbcdn.net/v/t39.2178-6/13421551_1702530599996541_471321650_n.png?oh=60b2566071cfb9662ce3c303d3ab3d8e&oe=5A4E859F)


# Wrapping it up

* Restart your bot server (the terminal running `npm start`) to begin receiving content from your FB messenger app. 

*Note: Do not restart ngrok as this will change your url!*

* On your FB page, click on the More Options (ellipsis) icon to the right of the Share button, then select `View as Page Visitor` in the dropdown menu

* Click on `Send Message`, type in a message, and confirm that your message has been echoed

Congrats, you just built a bot. Though, all it can do is repeat what it receives. It's up to you to break out of the echo chamber

Start expanding your bot's reliability, usability and functionality to craft compelling interactions that keep users engaged!

# Hosting

ngrok is helpful in rapid development, but its utility ends once your machine is turned off

Keep your bot continously alive and always ready to interact with users by hosting it on Heroku:

* [Deploy](https://devcenter.heroku.com/articles/getting-started-with-nodejs#introduction) your bot to Heroku.

* Set the `APP_SECRET`, `PAGE_ACCESS_TOKEN`, AND `VALIDATION_TOKEN` [config variables](https://devcenter.heroku.com/articles/config-vars).

* Return to the App Dashboard in your browser. Select `Webhooks` on the bottom left corner. Click on `Edit Subscription` and update your callback url to point to your Heroku url plus the `/webhook` route. 

*Troubleshooting: You may need to wait 5-10 minutes for Heroku to start serving your app.*
