## Project Summary
The goal of this project is to give you a taste of the environment and tools you will most likely come across in a front end role. Your focus should be to understand the role every tool and technology is playing in the overall architecture, but you shouldn’t feel the need to memorize the particular commands, config setups, or structure that we create here. Every company - and even every project - will have its own custom setup, but if you understand the moving pieces you will be able to get the gist of even far more complicated projects than this one.

## What You Will Build
We will be building web tool that allows users to run Natural Language Processing (NLP) on articles or blogs found on other websites. Using an exciting new api called Aylien, we can build a simple web interface to interact with their NLP system. This tool will give us back pertinent information about the article, like whether the content is subjective (opinion) or objective (fact-based) and whether it is positive, neutral, or negative in tone.

Node and express will be the webserver and routing, and webpack will be our build tool of choice. Using webpack, we will set up the app to have dev and prod environments, each with their own set of tools and commands.

More About Natural Language Processing
NLP is considered its own branch of computer science, focused on computers’ ability to process and even interact with natural human speech. Machine learning and deep learning are used on massive amounts of data to obtain the rules and understanding of nuance in human speech. Everyone who has used Alexa or Google Assistant or other voice command systems knows that they are always improving - but they aren’t perfect. Verbal interactions can be incredibly hard to decipher. Sarcasm, for instance, requires understanding not just words and grammar but tone as well, and regional accents and ways of saying things have to be taken into account, not to mention coverage for all the major languages

## Getting started
It would probably be good to first get your basic project setup and functioning. Follow the steps from the course up to Lesson 4 but don't add Service Workers just yet. We won't need the service workers during development and having extra caches floating around just means there's more potential for confusion. So, fork this repo and begin your project setup.

Remember that once you clone, you will still need to install everything:

cd into your new folder and run:

npm install
Setting up the API
The Aylien API is perhaps different than what you've used before. It has you install a node module to run certain commands through, it will simplify the requests we need to make from our node/express backend.

Step 1: Signup for an API key
First, you will need to go here. Signing up will get you an API key. Don't worry, at the time of this course, the API is free to use up to 1000 requests per day or 333 intensive requests. It is free to check how many requests you have remaining for the day.

Step 2: Install the SDK
Next you'll need to get the SDK. SDK stands for Software Development Kit, and SDKs are usually a program that brings together various tools to help you work with a specific technology. SDKs will be available for all the major languages and platforms, for instance the Aylien SDK brings together a bunch of tools and functions that will make it possible to interface with their API from our server and is available for Node, Python, PHP, Go, Ruby and many others. We are going to use the Node one, the page is available here. You get 1000 free requests per day. 

Step 3: Require the SDK package
Install the SDK in your project and then we'll be ready to set up your server/index.js file.

## our server index.js file must have these things:

[ ] Require the Aylien npm package
var aylien = require("aylien_textapi");
Step 4: Environment Variables
Next we need to declare our API keys, which will look something like this:

// set aylien API credentias
var textapi = new aylien({
  application_id: "your-api-id",
  application_key: "your-key"
});
...but there's a problem with this. We are about to put our personal API keys into a file, but when we push, this file is going to be available PUBLICLY on Github. Private keys, visible publicly are never a good thing. So, we have to figure out a way to make that not happen. The way we will do that is with environment variables. Environment variables are pretty much like normal variables in that they have a name and hold a value, but these variables only belong to your system and won't be visible when you push to a different environment like Github.

[ ] Use npm or yarn to install the dotenv package npm install dotenv. This will allow us to use environment variables we set in a new file
[ ] Create a new .env file in the root of your project
[ ] Go to your .gitignore file and add .env - this will make sure that we don't push our environment variables to Github! If you forget this step, all of the work we did to protect our API keys was pointless.
[ ] Fill the .env file with your API keys like this:
API_ID=**************************
API_KEY=**************************
[ ] Add this code to the very top of your server/index.js file:
const dotenv = require('dotenv');
dotenv.config();
[ ] Reference variables you created in the .env file by putting process.env in front of it, an example might look like this:
console.log(`Your API key is ${process.env.API_KEY}`);
...Not that you would want to do that. This means that our updated API credential settings will look like this:
// set aylien API credentials
// NOTICE that textapi is the name I used, but it is arbitrary.
// You could call it aylienapi, nlp, or anything else, 
//   just make sure to make that change universally!
var textapi = new aylien({
application_id: process.env.API_ID,
application_key: process.env.API_KEY
});
Step 5: Using the API
We're ready to go! The API has a lot of different endpoints you can take a look at here. And you can see how using the SDK simplifies the requests we need to make.

I won't provide further examples here, as it's up to you to create the various requests and make sure your server is set up appropriately.