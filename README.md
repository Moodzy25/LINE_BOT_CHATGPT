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
________________________________________________________________________________________________________________________________________________
service: specifies the name of the service. In this case, it is chatgpt-line-bot-serverless.
frameworkVersion: specifies the version of the Serverless Framework to be used.
custom: specifies any custom variables that are used in the file. In this case, it is reading the values from the .env.yml file.
provider: specifies the name of the cloud provider and the runtime version. It also defines the environment variables to be used by the function.
functions: specifies the function name, handler, timeout, and events. In this case, the function name is LineBot, the handler is main.lambda_handler, the timeout is set to 30 seconds, and the function is triggered by an HTTP POST request to the /webhook path.
plugins: specifies the plugins used by the Serverless Framework. In this case, it is using the serverless-python-requirements plugin to manage the Python dependencies.
Now, you can use the serverless framework to deploy your bot to AWS Lambda. You can do this by running the serverless deploy command from the command line.

After that, you’ll see something like this : 

Deploying chatgpt-line-bot-serverless to stage dev (us-east-1)

✔ Service deployed to stack chatgpt-line-bot-serverless-dev (78s)

endpoint: POST - https://xxxxxxxx.execute-api.us-east-1.amazonaws.com/dev/webhook
functions:
  LineBot: chatgpt-line-bot-serverless-LineBot (3.5 MB)

Improve API performance – monitor it with the Serverless Console: run "serverless --console"


Put this URL into Webhook URL on LINE Developers Platform.

That’s it! Your ChatGPT bot should now be up and running on LINE, ready to answer users' questions and provide helpful responses.

Author’s Note
This tutorial was written by ChatGPT.
