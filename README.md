# Nexmo and IBM Voice Agent with Watson

This repo will help you get started with connecting Nexmo to an IBM Voice Agent with Watson service orchestration engine. This will allow you to create complex flows to interact with your customers. 

## Setting up Node-RED

This sample project uses [Node-RED](https://nodered.org/) to create the connection between Nexmo and IBM Voice Agent with Watson.

1. Signup for [IBM Cloud account](https://nexmo.dev/ibm-account-signup) (if you don't already have one)
1. Create [Node-RED Starter](https://nexmo.dev/ibm-cloud-node-red) app in IBM Cloud
  1. This process can take a few minutes.
  1. Once complete, click `View App URL`
  1. Follow directions to setup Node-RED
1. Copy the `https://<app name>.mybluemix.net` part of the application for use in the next step.

## Create Nexmo Voice Application

You will need a Nexmo number and setup the voice application for this app. There are two ways to create an application with Nexmo - using the dashboard or the Nexmo CLI.  This section will cover both methods.

### Using the Dashboard

1. [Sign in](https://dashboard.nexmo.com/sign-in) or [create](https://dashboard.nexmo.com/sign-up) a Nexmo account
1. [Buy a new virtual number](https://dashboard.nexmo.com/buy-numbers)
1. [Create a voice application](https://dashboard.nexmo.com/voice/create-application)
1. Add the event url - `https://<app name>.mybluemix.net/eventURL`
1. Add the answer url - `https://<app name>.mybluemix.net/answerURL`
1. Click `Create Application`
1. Click `Numbers` and link the recently created virtual number.
1. Copy the virtual number for use in the next step.

## Setting up the Voice Agent

Next you will need to create the Voice Agent in IBM Cloud. Copy the virtual number you created in in Nexmo for this step.

1. Create an [IBM Voice Agent with Watson](https://cloud.ibm.com/catalog/services/voice-agent-with-watson)
1. Click `Manage` and then `Create a voice agent`
1. Give your agent a name, and paste the Nexmo number in the `Phone number` field.
1. Under Watson Assistant:
  1. Copy the workspace ID and store it for the Node-RED setup.
  1. Change the `Service type` to `Service orchestration engine`
  1. Add the url `https://<app name>.mybluemix.net/soe`
  1. Enter your username and password from Node-RED
1. Click `Create voice agent`
1. Navigate to `Getting Started` and copy your SIP endpoint and add your phone number to it like so: `sip:15555555555@us-south.voiceagent.cloud.ibm.com`

## Create Node-RED Flow

### Import Flow

There is a sample flow you can import and begin using right away.  

1. Open `NodeRED-Nexmo-SOE.json` and copy the entire contents.
1. Open your Node-RED application.
1. In the top right menu find `Import > Clipboard`
1. Paste the json into the window, select `New Flow` and click `Import`.

### Setup Watson Assistant Node

During the Voice Agent setup, it created a Watson Assistant service.  Locate this in your IBM Cloud account.

1. Copy the `API Key` and the `URL`
1. In Node-RED, locate the `Watson Assistant` node, and paste in the `API Key`, paste the `URL` to `Service Endpoint`, and the `Workspace ID` you received during the last step.
1. Click `Done`

### Setup Nexmo Connect Node

1. Locate the `Connect` node, and open it.
1. Paste your SIP endpoint into the `URI` field.
1. Add your virtual number to the `From` field.

## Test it Out
Once all configuration is complete, click the `Deploy` button in node red to push the flow live.

Dial your virtual phone number.  You will hear `Please wait while we connect you.` followed by the Watson Voice Assistant telling you about Voice Agent.

## Extend

To take this further, you will want to build your own Voice Assistant skill set with intents and dialog.  You can listen for these with a Node-RED switch and build flows and sub-flows to manage each specific intent.
