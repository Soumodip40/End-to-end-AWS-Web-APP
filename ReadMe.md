## End to End Serverless Web Application 
I have created one end-to-end web application from scratch, in this project i have used total 5 services.
![webapp](https://github.com/Soumodip40/End-to-end-AWS-Web-APP/assets/128739966/c71cefba-be5a-4fe5-afba-3e883c82328d)

1. Open Notepad on your computer. Create a new file and paste the following HTML in it:
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>To the Power of Math!</title>
</head>

<body>
    To the Power of Math!
</body>
</html>

## Create a webapp with amplify console

2. Save the file as index.html.

3. ZIP (compress) only the HTML file.

4. In a new browser window, log into the Amplify console. Note: We will be using the Oregon (us-west-2) Region for this tutorial.

5. In the Get Started section, under Host your web app, choose the orange Get started button.

6. Select Deploy without Git provider. This is what you should see on the screen:

7. Choose the Continue button.

8. In the App name field, enter GettingStarted.

9. For Environment name, enter dev.

10. Select the Drag and drop method. This is what you should see on your screen:

11. Choose the Choose files button.

12. Select the ZIP file you created in Step 3.

13. Choose the Save and deploy button.

14. After a few seconds, you should see the message Deployment successfully completed.
## Test your Webapp
1. Select Domain Management in the left navigation menu.
2. Copy and paste the URL displayed in the form into your browser.

Your web app will load in a new browser tab and render "Power Of Math" Congratulations!


## Create and config lambda function

1. In a new browser tab, log in to the AWS Lambda console.
2. Make sure you create your function in the same Region in which you created the web app in the previous module. You can see this at the very top of the page, next to your account name.
Choose the orange Create function button.
3. Under Function name, enter heloow world function

4. Select Python 3.8 from the runtime dropdown and leave the rest of the defaults unchanged.

5. Select Python 3.8 from the runtime dropdown and leave the rest of the defaults unchanged.

6. Choose the orange Create function button.

7. You should see a green message box at the top of your screen with the following message "Successfully created the function HelloWorldFunction."

8. Under Code source, replace the code in lambda_function.py with the following:

> #import the JSON utility package

> import json

> #import the Python math library

> import math

> #define the handler function that the Lambda service will use an entry point

> def lambda_handler(event, context):

> #extract the two numbers from the Lambda service's event object

    mathResult = math.pow(int(event['base']), int(event['exponent']))

    # return a properly formatted JSON object
    return {
    'statusCode': 200,
    'body': json.dumps('Your result is ' + str(mathResult))
    }



9. Save by going to the file menu and selecting Save to save the changes.

10. Choose Deploy to deploy the changes.

11. Let's test our new function. Choose the orange Test button to create a test event by selecting Configure test event.

12. Under Event name, enter HelloWorldTestEvent.
13. Copy and paste the following JSON object to replace the default one:

{
"base": "2",
"exponent": "4"
}

14. Choose the Save button at the bottom of the page.

## Test your lambda function

1.Under the HelloWorldFunction section at the top of the page, select Test tab.
2.You should see a light green box at the top of the page with the following text: Execution result: succeeded. You can choose Details to see the event the function returned.
3.Well done! You now have a working Lambda function.



## Create a new Rest API 

1. Log in to the API Gateway console.
2. In the Choose an API type section, find the REST API card and choose the Build button on the card.
3. Under Choose the protocol, select REST.
4. Under Create new API, select New API.
5. In the API name field, enter HelloWorldAPI.
6. Select Edge optimized from the Endpoint Type dropdown. (Note: Edge-optimized endpoints are best for geographically distributed clients. This makes them a good choice for public services being accessed from 
7. the internet. Regional endpoints are typically used for APIs that are accessed primarily from within the same AWS Region.)
Choose the blue Create API button.

## Create a new resource and method

1. In the left navigation pane, select Resources under API: HelloWorldAPI.
2. Ensure the "/" resource is selected.
3. From the Actions dropdown menu, select Create Method.
4. Select POST from the new dropdown that appears, then select the checkmark.
5. Select Lambda Function for the Integration type.
6. Select the Lambda Region you used when making the function (or else you will see a warning box reading "You do not have any Lambda Functions in...").
7. Enter HelloWorldFunction in the Lambda Function field.
8. Choose the blue Save button.
9. You should see a message letting you know you are giving the API you are creating permission to call your Lambda function. Choose the OK button.
10. With the newly created POST method selected, select Enable CORS from the Action dropdown menu.
11. Leave the POST checkbox selected and choose the blue Enable CORS and replace existing CORS headers button
12. You should see a message asking you to confirm method changes. Choose the blue Yes, replace existing values button.


## Deploy API

1. In the Actions dropdown list, select Deploy API.
2. Select [New Stage] in the Deployment stage dropdown list.
3. Enter dev for the Stage Name.
4. Choose Deploy.
5. Copy and save the URL next to Invoke URL (you will need it in module five).


## Validate API

1. In the left navigation pane, select Resources.
2. The methods for our API will now be listed on the right. Choose POST.
3. Choose the small blue lightning bolt.
4. Paste the following into the Request Body field:
{
    "base":"2",
    "exponent":"4"
}


5. Choose the blue Test button.

6. On the right side, you should see a response with Code 200.

7. Great! We have built and tested an API that calls our Lambda function.


## Create a DynanoDB

1.Log in to the Amazon DynamoDB console.
2.Make sure you create your table in the same Region in which you created the web app in the previous module. You can see this at the very top of the page, next to your account name.
3.Choose the orange Create table button.
4.Under Table name, enter HelloWorldDatabase.
5.In the Partition key field, enter ID. The partition key is part of the table's primary key.
6.Leave the rest of the default values unchanged and choose the orange Create table button.
7.In the list of tables, select the table name, HelloWorldDatabase.
8.In the General information section, show Additional info by selecting the down arrow.
9.Copy the Amazon Resource Name (ARN). You will need it later in this module.

## Create and add IAM policy

1.Now that we have a table, let's edit our Lambda function to be able to write data to it. In a new browser window, open the AWS Lambda console.
2.Select the function we created in module two (if you have been using our examples, it will be called HelloWorldFunction). If you don't see it, check the Region 3.dropdown in the upper right next to your name to ensure you're in the same Region you created the function in.
4.We'll be adding permissions to our function so it can use the DynamoDB service, and we will be using AWS Identity and Access Management (IAM) to do so.
5.Select the Configuration tab and select Permissions from the right side menu.
6.In the Execution role box, under Role name, choose the link. A new browser tab will open.
7.In the Permissions policies box, open the Add permissions dropdown and select Create inline policy.
8.Select the JSON tab.
9.Paste the following policy in the text area, taking care to replace your table's ARN in the Resource field in line 15:

{
"Version": "2012-10-17",
"Statement": [
    {
        "Sid": "VisualEditor0",
        "Effect": "Allow",
        "Action": [
            "dynamodb:PutItem",
            "dynamodb:DeleteItem",
            "dynamodb:GetItem",
            "dynamodb:Scan",
            "dynamodb:Query",
            "dynamodb:UpdateItem"
        ],
        "Resource": "YOUR-TABLE-ARN"
    }
    ]
}
