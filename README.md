<a href="https://www.twilio.com">
  <img src="https://static0.twilio.com/marketing/bundles/marketing/img/logos/wordmark-red.svg" alt="Twilio" width="250" />
</a>

# Warm Transfer

[![Build Status](https://travis-ci.org/TwilioDevEd/warm-transfer-node.svg?branch=master)](https://travis-ci.org/TwilioDevEd/warm-transfer-node)

Have you ever been disconnected from a support call while being transferred to another support agent? Warm transfer eliminates this problem. Using Twilio powered warm transfers your agents will have the ability to conference in another agent in realtime.

Twilio powered warm transfers your agents will have the ability to dial in another agent in real-time.

Here is how it works at a high level:

1. The first agent becomes available when they connect through the web client.
2. The second agent also becomes available when they connect through the web client.
3. A client calls our support line.
4. The client stays on hold while the first agent joins the call.
5. While the first agent is on the phone with the client, they can dial a second agent into the call.
6. Once the second agent is on the call, the first one can disconnect from it. This way the client and the second agent stay on the call.

[Read the full tutorial here](https://www.twilio.com/docs/tutorials/walkthrough/warm-transfer/node/express)!

## Requirements:
* [Node](http://nodejs.org/)
* [MongoDb](http://docs.mongodb.org/manual/installation/)

## Local development

1. First clone this repository and `cd` into it.

   ```bash
   git clone git@github.com:TwilioDevEd/warm-transfer-node.git
   cd warm-transfer-node
   ```

1. Copy the sample configuration file and edit it to match your configuration.

   ```bash
   $ cp .env.example .env
   ```

  You can find your `TWILIO_ACCOUNT_SID` and `TWILIO_AUTH_TOKEN` in your
  [Twilio Account Settings](https://www.twilio.com/user/account/settings).
  You will also need a `TWILIO_NUMBER`, which you may find [here](https://www.twilio.com/user/account/phone-numbers/incoming).

1. Install dependencies.

  ```bash
  $ npm install
  ```

1. Make sure the tests succeed.

  ```bash
  $ npm test
  ```

1. Run the application.

  ```bash
  $ npm start
  ```

1. Expose your application to the wider internet using [ngrok](http://ngrok.com). This step
  is important because the application won't work as expected if you run it through
  localhost.

  ```bash
  $ ngrok http 3000
  ```

  Once ngrok is running, open up your browser and go to your ngrok URL. It will
  look something like this:

  `http://9a159ccf.ngrok.io`

  You can read [this blog post](https://www.twilio.com/blog/2015/09/6-awesome-reasons-to-use-ngrok-when-testing-webhooks.html)
  for more details on how to use ngrok.

1. Configure Twilio to call your webhooks

  You will also need to configure Twilio to call your application when calls are received on your `TWILIO_NUMBER`. The voice URL should look something like this:

  ```
  http://<your-ngrok-subdomain>.ngrok.io/conference/connect/client
  ```

  ![Configure Voice](http://howtodocs.s3.amazonaws.com/twilio-number-config-all-med.gif)

1. Check it out at [http://localhost:3000](http://localhost:3000).

That's it!

## How to Demo

1. Navigate to `https://<your_ngrok_subdomain>.ngrok.io` in two different
   browser tabs or windows.

   **Notes:**
   * Remember to use your SSL enabled ngrok URL `https`.
   Failing to do this won't allow you to receive incoming calls.

   * The application has been tested with [Chrome](https://www.google.com/chrome/)
   and [Firefox](https://firefox.com). Safari is not supported at the moment.

1. In one window/tab click `Connect as Agent 1` and in the other one click
   `Connect as Agent 2`. Now both agents are waiting for an incoming call.

1. Dial your [Twilio Number]() to start a call with `Agent 1`. Your `TWILIO_NUMBER`
   environment variable was set when configuring the application to run.

1. When `Agent 1` answers the call from the client, he/she can dial `Agent 2` in
   by clicking on the `Dial agent 2 in` button.

1. Once `Agent 2` answers the call all three participants will have joined the same
   call. After that `Agent 1` can drop the call and leave both the client and `Agent 2`
   having a pleasant talk.

## Meta

* No warranty expressed or implied. Software is as is. Diggity.
* [MIT License](http://www.opensource.org/licenses/mit-license.html)
* Lovingly crafted by Twilio Developer Education.
