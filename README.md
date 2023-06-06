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
13. Save and return to the build interface. 
14. Open a new tab and go to https://console.aws.amazon.com/. Log in with your AWS account.
15. In the search bar at the top of the page, type in "Lambda" and press enter.
16. Click on "Create Function" at the top right of the page. 
17. Name your function and set the runtime to `python 3.10`.
18. On the Lambda function page, click on "Add Trigger". Set the source to "Alexa".
19. Go back to the skill build interface (the other tab) and click on "Endpoint" on the right hand pane.
20. Copy the Skill ID to the keyboard and go back to the Lambda function page. Paste the skill ID into the box.
21. Click "Add" and the lambda function should now be connected to your Alexa Skill. 
