# Project Showcase: Sending Emails with AWS Lambda and SES 📧

I want to share a little exercise I practiced today, something I already did on the AWS laboratories during the AWS re/Start programme. With this exercise I learned to send emails using AWS Lambda and Amazon SES (Simple Email Service). Here's a detailed overview of what I did and what I learned.

🔎 **Steps to Send an Email Using AWS Lambda and SES:**

1. **Set Up SES:**

   - In the AWS Console, search for SES.
     ![1.png](Project%20Showcase%20Sending%20Emails%20with%20AWS%20Lambda%20an%2053e896678a1c4c49b1585e2c8723c622/1.png)
   - Create an Identity for your email address.
     ![Diseño sin título (5).jpg](<Project%20Showcase%20Sending%20Emails%20with%20AWS%20Lambda%20an%2053e896678a1c4c49b1585e2c8723c622/Diseo_sin_ttulo_(5).jpg>)
     ![3.png](Project%20Showcase%20Sending%20Emails%20with%20AWS%20Lambda%20an%2053e896678a1c4c49b1585e2c8723c622/3.png)
   - Verify your email by checking your inbox.
     ![4.png](Project%20Showcase%20Sending%20Emails%20with%20AWS%20Lambda%20an%2053e896678a1c4c49b1585e2c8723c622/4.png)
     ![5.png](Project%20Showcase%20Sending%20Emails%20with%20AWS%20Lambda%20an%2053e896678a1c4c49b1585e2c8723c622/5.png)
     ![6.png](Project%20Showcase%20Sending%20Emails%20with%20AWS%20Lambda%20an%2053e896678a1c4c49b1585e2c8723c622/6.png)
     ![7.png](Project%20Showcase%20Sending%20Emails%20with%20AWS%20Lambda%20an%2053e896678a1c4c49b1585e2c8723c622/7.png)

1. **Create IAM Role:**

   - Go to IAM (Identity and Access Management) in the AWS Console.
     ![8.png](Project%20Showcase%20Sending%20Emails%20with%20AWS%20Lambda%20an%2053e896678a1c4c49b1585e2c8723c622/8.png)
   - Create a role for Lambda with Amazon SES Full Access.
     ![Diseño sin título (6).jpg](Project%20Showcase%20Sending%20Emails%20with%20AWS%20Lambda%20an%2053e896678a1c4c49b1585e2c8723c622/97a02a19-dc07-450c-95e4-ce915153e9c0.png)
     ![10.png](Project%20Showcase%20Sending%20Emails%20with%20AWS%20Lambda%20an%2053e896678a1c4c49b1585e2c8723c622/10.png)
     ![11.png](Project%20Showcase%20Sending%20Emails%20with%20AWS%20Lambda%20an%2053e896678a1c4c49b1585e2c8723c622/11.png)
     ![12.png](Project%20Showcase%20Sending%20Emails%20with%20AWS%20Lambda%20an%2053e896678a1c4c49b1585e2c8723c622/12.png)

1. **Create Lambda Function:**
   - In the AWS Console, search for Lambda and create a new function.
     ![Diseño sin título (7).jpg](Project%20Showcase%20Sending%20Emails%20with%20AWS%20Lambda%20an%2053e896678a1c4c49b1585e2c8723c622/fe7e6f10-3391-4d06-9c78-59492810b082.png)
   - Name your function and choose Python as the runtime.
     ![15.png](Project%20Showcase%20Sending%20Emails%20with%20AWS%20Lambda%20an%2053e896678a1c4c49b1585e2c8723c622/15.png)
   - Assign the IAM role you created earlier to the Lambda function and hit “Create Function”.
     ![16.png](Project%20Showcase%20Sending%20Emails%20with%20AWS%20Lambda%20an%2053e896678a1c4c49b1585e2c8723c622/16.png)
1. **Write the Code:**

   ```python
   import json
   import boto3

   def lambda_handler(event, context):
       client = boto3.client("ses")
       subject = "Test Subject from Lambda"
       body = "Test body from Lambda"
       message = {
           "Subject": {"Data": subject},
           "Body": {"Html": {"Data": body}}
       }
       response = client.send_email(
           Source="xyz@gmail.com",
           Destination={"ToAddresses": ["xyz@gmail.com"]},
           Message=message
       )
       return response
   ```

   - Use the `boto3` library to interact with AWS services.
   - Define the SES client and construct the email subject and body.
   - Use the `send_email` method to send the email.
     ![17.png](Project%20Showcase%20Sending%20Emails%20with%20AWS%20Lambda%20an%2053e896678a1c4c49b1585e2c8723c622/17.png)

1. **Deploy and Test:**
   - Deploy your Lambda function. You need to always deploy after any changes to the function before testing.
   - Create and run a test event to see the email in your inbox.
     ![18.png](Project%20Showcase%20Sending%20Emails%20with%20AWS%20Lambda%20an%2053e896678a1c4c49b1585e2c8723c622/18.png)
   - Here you can see that the function worked and there isn’t any error.
     ![19.png](Project%20Showcase%20Sending%20Emails%20with%20AWS%20Lambda%20an%2053e896678a1c4c49b1585e2c8723c622/19.png)
   - Check your email for the email. (Don’t forget to check your spam folder!)
     ![20.png](Project%20Showcase%20Sending%20Emails%20with%20AWS%20Lambda%20an%2053e896678a1c4c49b1585e2c8723c622/20.png)

→ **What I Learned:**

- **AWS Lambda**: How to create and deploy serverless functions.
- **Amazon SES**: How to set up and use SES for sending emails.
- **IAM Roles**: How to manage permissions and roles in AWS.
- **Boto3**: Using AWS SDK for Python to interact with AWS services.

→ **AWS Services Used:**

- **AWS Lambda**: For running code without provisioning servers.
- **Amazon SES**: For sending and receiving emails.
- **IAM**: For managing access to AWS services securely.

This project was a fantastic learning experience, helping me understand the power of serverless architectures and cloud-based email services.
