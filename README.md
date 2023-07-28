# LINE_BOT_CHATGPT
Build a ChatGPT LINE bot
In this tutorial, we will learn how to create a chatbot using the ChatGPT model from OpenAI, and deploy it on the LINE messaging platform using the Serverless Framework.

Code is here

Prerequisites
An OpenAI API key
A LINE developer account
AWS CLI
Serverless Framework
Python 3.8 or later
Step 1: Create a new Serverless Service
Create a new Serverless service using the Serverless Framework by running the following command:

sls create --template aws-python3 --path chatgpt-line-bot-serverless
This will create a new directory called chatgpt-line-bot-serverless with some boilerplate code in it.

Step 2: Set up the Environment Variables
Create a .env.yml file in the project directory and add the following environment variables:

openaiKey: <OPENAI_API_KEY>
lineChannelSecret: <LINE_CHANNEL_SECRET>
lineChannelAccessToken: <LINE_CHANNEL_ACCESS_TOKEN>
Make sure to replace <OPENAI_API_KEY>, <LINE_CHANNEL_SECRET>, and <LINE_CHANNEL_ACCESS_TOKEN> with your own API keys and secrets.

Step 3: Install Dependencies
To use OpenAI and LINE APIs in your Python code, you need to install their respective libraries. You can do this by running the following command:

cd chatgpt-line-bot-serverless
python3.8 -m venv ./venv
source ./venv/bin/activate
pip install openai line-bot-sdk
Also install serverless plugin.

npm init -y
npm install --save serverless-python-requirements
This will install the plugin that manages your Python dependencies.

Step 4: Write the Code
Create a file named main.py in the chatgpt-line-bot-serverless directory.

This code creates a Lambda function that uses OpenAI’s GPT-3 model to generate responses to user messages. The code also handles LINE webhook events. (YOU CAN SEE IN FOLDER main.py)

____________________________________________________________________________________________________________________________________________
The code starts by importing the necessary modules and setting up some global variables, including the LINE and OpenAI API credentials and a conversation history.
The lambda_handler function is the main entry point for the serverless function. It listens for incoming HTTP requests from LINE and passes them on to the handler object, which is responsible for processing LINE events.
The ask_chatgpt function sends a user’s message to the OpenAI API and generates a response. It then appends the user’s message and the response to the conversation history.
The handling_message function is called whenever a user sends a message to the bot. It extracts the message from the event object, passes it to the ask_chatgpt function to generate a response, and then sends that response back to the user via LINE.

Step 5: Deploy your bot
This serverless.yml file is used to configure and deploy the Lambda function to AWS using the Serverless Framework. (see folder)
