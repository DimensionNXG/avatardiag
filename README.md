# avatardiag

UNEEQ has inbuilt support for Google's DialogFlow. We can directly include question and answers just like a text based chatbot and avatar provided by UNEEQ will try to lipsynch to the words that looks real. 

## Example Get Token Node App
The purpose of this application is to return a single use token as generated by the UneeQ API server, using a private 
token which is secret to this application. By generating tokens in this way, customer secrets can be kept securely
within this application and not exposed via an HTML front end application.

#### Dependencies
- Node version 8 or higher
- NPM version 6 or higher

#### Running Locally
`npm i` to install dependencies from package.json.
<br/>
`npm start` to run the application locally which will expose the application on http://localhost:3000
<br/><br/>
Environment variables are configurable via `.env` and will be provided to you.
- `UNEEQ_URI` The UneeQ server you will retrieve the token from.
- `UNEEQ_SECRET` The UneeQ secret used to secure the token request.
- `UNEEQ_WORKSPACE` The conversation workspace you want to generate a token for. A token will only be able to start a 
session for the conversation workspace if you generated the token using the same workspace id. The workspace
conversation follows GUID format (e.g. 5d4f1723-4f23-4086-bf91-00b1e58da7f8).

Once the application is running you can request a token by performing a GET request to http://localhost:3000/token
To test the application is running you can perform a GET request to http://localhost:3000/ping and expect the response
'pong'.

#### Tests
To run unit tests use the command `npm test`. Mocha + Chai frameworks are used.

#### Docker
Build Image: `docker build -t examples/node-token-example .`
<br/>
Run Image: `docker run -p 3000:3000 examples/node-token-example`


## Example Digital Human Web Frontend (node)
The purpose of this application is to demonstrate how to create a basic web frontend using the uneeq-js NPM package
(https://www.npmjs.com/package/uneeq-js).

This demo supports the following:
- Retrieval of a session token used to create a UneeQ session.
- Creation of a UneeQ session with uneeq-js npm package.
- Establishment of a UneeQ digital human video stream.
- Push to talk (spacebar) to speak to the digital human.
- Handling of user speech to text messages and display on screen.
- Handling of digital human answer messages and display on screen.

#### Dependencies
- Node version 8 or higher
- NPM version 6 or higher
- [Session token service](https://gitlab.com/uneeq-oss/examples/tree/master/token/node)

#### Running Locally

<b>Installing a webserver:</b>
<br/>
To run the web example you will need to serve index.html over a webserver. You can setup your own, or use the one 
configured in the example. To use http-server configured in the example you will need to install it as a global node
module first:<br/>
`npm install --global http-server`

<b>Installing dependencies:</b>
<br/>
To install dependencies from package.json:<br/>
`npm install` 

<b>Environment Variables:</b>
main.js contains three environment variables:
- `GET_TOKEN_URL` The customer built token service.
- `UNEEQ_URL` The UneeQ server you will retrieve the token from.
- `UNEEQ_WORKSPACE` The conversation workspace you want to generate a token for.

`UNEEQ_URL` & `UNEEQ_WORKSPACE` should match values used to generate token. Be sure to update these values before
running the example app, this can be done in main.js

<b>Running the application:</b>
<br/>
The following command will compile bundle.js and run the webserver. bundle.js is imported into index.html and includes the uneeq-js library. This will
watch for changes to main.js and recompile bundle.js automatically (using watchify). The webserver will run on 127.0.0.1
and serve index.html:<br/>
`npm start`

Once compiled, open localhost:8080 in your web browser. Clicking the 'Start Digital Human' button will cause the page to
request a session token from your token service. Once a token is retrieved it will be used to start a digital human
session. After a few seconds you will see the digital human on screen. You can press and hold the spacebar key to speak
to the digital human.

Your browsers javascript console will log any errors that occur.
