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
3. Under Function name, enter 
 #import the JSON utility package
import json
#import the Python math library
import math

#define the handler function that the Lambda service will use an entry point
def lambda_handler(event, context):

#extract the two numbers from the Lambda service's event object
    mathResult = math.pow(int(event['base']), int(event['exponent']))

    # return a properly formatted JSON object
    return {
    'statusCode': 200,
    'body': json.dumps('Your result is ' + str(mathResult))
    }

