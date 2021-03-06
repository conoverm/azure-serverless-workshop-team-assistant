# GitHub Issue Bot 

In this part of the workshop you will extend our bot with the capability to create an issue in GitHub. 
We will build a logic app with 3 steps. We will use Request / Response Step Connector for invoking the Logic App and providing the final response where our second step will be creating a GitHub issue.
Please refer to the diagram below showing the steps in logic app.

![Architecture](Content/Images/1-Architecutre.png)

## Features

This project  provides the following features:

* Create GitHub Issue 
* Provide link to the created GitHub issue in the response 

## Getting Started

### Prerequisites

1.	You need to have GitHub account, if you don’t please create one here https://github.com

2.	Access to Azure Subscription, please check here https://portal.azure.com

3. Bot Framework Emulator - https://github.com/Microsoft/BotFramework-Emulator/releases/

### Walkthrough 

- Login to Azure Portal and Create new Logic App

  - If you don’t see it on your left menu you can search for it via More Services on the bottom
  
  ![Azure Menu](Content/Images/2-AzureLogicApps.png)
  
  - Then type Logic Apps in the Search Bar 
  
  ![Logic App Search](Content/Images/3-AzureMenu.png)
  
  - Press Add button
  
  ![Add Logic App](Content/Images/4-AzureCreateLogicApp.png)
  
  - And fill the required data and press Create button at the bottom
  
  ![Logic App Parameters](Content/Images/5-LogicAppParameters.png)
  
- Next, we will configure the Logic App. In the Logic Apps Designer please select “Blank Logic App” from the Templates section
  
  ![Logic App Parameters](Content/Images/6-LogicAppBlankTemplate.png)
  
  - In the Connector Search select Request / Response Connector
  
   ![Logic App Request](Content/Images/7-LogicAppRequest.png)
   
   - Press “Use sample payload to generate schema” button
   
   ![Logic App Request Body](Content/Images/8-LogicAppRequestBody.png)
   
   - And paste the following JSON
   
      ```javascript
      {
        "title": "My new issue",
        "text":  "My new issue description"
      }
      ```
    
    - The contron should look like the picture below. Next press Done 
    
   ![JSON object](Content/Images/9-LogicAppJsonObject.png)
   
    - The result will look like 
   
   ![JSON schema](Content/Images/10-JsonSchema.png)
   
    - Then press “New Step” button, select “Add an action” and select GitHub Connector with Action – “Create an issue”
   
    ![Github step](Content/Images/11-GitHub.png)
   
     - Next, please select Sign In and input your GitHub account credentials and fill the required data that will be used for creating the GitHub issue
   
    ![Github data](Content/Images/12-GitHubFields.png)
   
     - For title and body will pick dynamic content fields - title and text. Also set the correct repository and its owner.    
     
     ![Github dynamic data](Content/Images/13-GitHubDyniamicValues.png)
     
     - Press “New step” and search for Response and select Request - Response step:
     
     ![Slack post message](Content/Images/21-RequestResponse.PNG)
  
     - Next we will configure the step by selecting 200 for response code, specifying the repository and its owner. It is also very important to define the body with the following json object. Squire bot will expect message propery in the body object to display the final message to the user:
     
  ```javascript
  {
  
   	"message": "[GitHub Issue Link](https://github.com/{input-repo-owner}/{input-repo}/issues/@{body('Create_an_issue')?['number']})"

  }
  ```

    - We use dynamic value for issue ID when constructing the link. We use Markdown format for the message content:
   
      ![Slack post message](Content/Images/14-Slack.png)
     
    - Save your work and now you are ready to test. Go to the Request / Response connector step and copy the URL
      ![URL capturing](Content/Images/16-URL.png)
      
    - If you want to your logic app immediatelly, go to Postman or similar app and POST to the provided URL. Do not forget to set Content-Type header to “application/json”
   
       ![Postman testing 1](Content/Images/17-Postman1.png)
       
     - For the body use the JSON schema we defined several steps ago 
       ![Postman testing 2](Content/Images/18-Postman2.png)
       
     - You should receive the following reponse in Postman:
        ![Slack post](Content/Images/19-SlackPost.png)
        
     - You can go to your Logic App home screen and see the history of execution and troubleshoot 
       ![Logic app executions](Content/Images/20-LogicAppsRuns.png)
       
     - Now it is time to integrate GitHub Bot with the Squire Bot. Please follow the instructions for running locally the Squire Bot. And then copy the POST URL of the logic app we created in order to setup new task for Squire Bot. It should look very similar to the image below:
      ![Squire Bot GitHub Setup](Content/Images/23-SquireBotSetup.PNG)
      
     - Next start Bot Framework Emulator and connect to http://localhost:7071/api/bot . And now are you are ready to test GitHub Issuer via the Squire Bot. Please type the name of the task you created to start the conversation and the interaction should be very similar to the screenshot below:
     
     ![Squire Bot GitHub Task Test](Content/Images/22-BotConversation.PNG)
     
    
     - And if you click on the link in the last message you will be able to open the GitHub Issue we just created via Squire Bot:
     
       ![GitHub Issue](Content/Images/24-GitHubIssueCreated.PNG)
     
 Congratulations! You competed the module! 
 
 You have just added GitHub issue creation as a new capability of our always improving bot!
 
 Thank you!
   
   

