# AlexaGPT

Artificial Intelligence (GPT) Implementation into Alexa Home devices.

The following `python`-based program uses the Alexa Skill Developer Console, AWS Lambda, and AWS Cloud9, and the OpenAI API.

## Requirements 

1. OpenAI API Key: You can sign up for a billing account on the OpenAI website (https://platform.openai.com/) to recieve an API Key.
2. An AWS account with the necessary permissions to create and manage Lambda functions and Cloud9 environments. You can sign up for an account at https://portal.aws.amazon.com/billing/signup?type=enterprise#/start/email.
3. The Alexa Developer Console account for creating and configuring the skill. You can sign up for an account at https://developer.amazon.com/en-US/alexa/alexa-skills-kit.

## Installation and Setup

1. Begin by logging into the Alexa Skill Developer Console using your developer account.
2. Create a new skill and choose a name and primary locale. 
3. Choose the "other" experience option, a "custom" model, and create an "Alexa-Hosted (Python)" skill.
4. Make sure to choose the hosting region closest to you at the very bottom of the page.
5. Next, choose a "Start from Scratch" template and click "Create Skill".
6. In the right hand section, click on "Invocation Name". Set the invocation name to what you want to say to Alexa to activate the skill. The invocation name has to be mutliple words or abbreviated (Ex. "g. p. t." or "a. i."). Make sure to save the changes.
7. Click on the "Build" tab to return to the build interface.
8. On the left hand console, click on "Interaction Model" and choose "Intents (6)" in the dropdown menu.
9. On the Intents page, you should see 5 required built-in intents and a custom intent titled "HelloWorldIntent".
10. In the "ACTIONS" column for "HelloWorldIntent", click on "edit". Delete all of the sample utterances for the intent.
11. Add a sample utterance: "I want to you to {Query}". Create a new slot named "Query" and click enter to add the utterance.
12. Set the slot type to be "AMAZON.SearchQuery".
13. Save, click "Build Skill", and return to the build interface. 
14. Open a new tab and go to https://console.aws.amazon.com/. Log in with your AWS account.
15. In the search bar at the top of the page, type in "Lambda" and press enter.
16. Click on "Create Function" at the top right of the page. 
17. Name your function and set the runtime to `python 3.10`.
18. On the Lambda function page, click on "Add Trigger". Set the source to "Alexa".
19. Go back to the skill build interface (the other tab) and click on "Endpoint" on the right hand pane.
20. Copy the Skill ID to the keyboard and go back to the Lambda function page. Paste the skill ID into the box.
21. Click "Add" and the lambda function should now be connected to your Alexa Skill. 
22. Scroll down the page and click on the "Upload Code" dropdown menu. Choose ".zip file".
23. Download the `lambda_function.py` file from the repository. Compress the file `lambda_function.py` and upload it to the AWS Lambda Console.
24. Once uploaded, insert your OpenAI API Key in the following line in the code and deploy it to save your changes:
```python
openai.api_key = "OPENAI KEY HERE"
```
25. Open the AWS Console Home on a new tab and search up "Cloud9".
26. Click "Create Environment", name it, and click "Add".
27. In the terminal at the bottom of the page, install Python 3.8 and pip3 by running the following commands:
```bash
$ sudo amazon-linux-extras install python3.8
$ curl -O https://bootstrap.pypa.io/get-pip.py
$ python3.8 get-pip.py --user
```
27. Create a python folder by running the following command:
```bash
$ mkdir python
```
28. Install the `openai`, `boto3`, and `ask-sdk-core` libararies by running the following commands:
```bash
$ python3.8 -m pip install openai -t python/
$ python3.8 -m pip install boto3 -t python/
$ python3.8 -m pip install ask-sdk-core -t python/
```
29. Zip the contents of the python folder into a layer.zip file by running the following command:
```bash
$ zip -r layer.zip python
```
30. Publish the Lambda layer by running the following command. Replace "us-east-1" with the AWS Region that your Lambda function is in. You can find the AWS region of your lambda function by looking at its function ARN (Amazon Resource Name) on the Lambda console page. 
```bash
$ aws lambda publish-layer-version --layer-name pandas-layer --zip-file fileb://layer.zip --compatible-runtimes python3.8 --region us-east-1
```
31. Copy the `VersionARN` from the resulting output. Head back to the Lambda console and scroll down and click "Add a Layer".
32. Click on "Specify an ARN" and paste the `VersionARN` into the box. Click "Add". Scroll back up and click on "Deploy" to publish the code. If the button is not highlighted, then don't worry.
33. Scroll up to the top of the Lambda function console page and copy the Function ARN. 
34. Return to the Alexa Skill Build interface and click on "Endpoint" in the section on the right. 
35. Paste the Function ARN next to "Default Region" and click "Save".
36. Build the skill.

## Usage

Once the skill is built and the code is deployed, it can be tested on any Alexa home device connected to the email used to register for the skill developer account. If you don't have an Alexa device, then you can either test it on the mobile Alexa application or in the developer console under the "Test" tab. Make sure to set the skill state to "Development".

Without any customization, the interaction between the device and the user will look like this:
> **User**: Alexa, [Invocation Name].

> **Alexa**: Hello, this is GPT! What would you like me to do?

> **User**: I want you to {Query}.

> **Alexa**: *gpt-3.5-turbo response to {Query}*

The {Query} represents the text that is given to the OpenAI API, so it is important that the response is structured ***exactly*** in that manner. Example responses could be "I want you to **write me a poem about bananas**" or "I want you to **tell me how to bake a cheesecake**".

## Customization
