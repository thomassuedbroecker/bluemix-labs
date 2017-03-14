![](./images/conversation_icon_new.png)

# Introduction

With the Watson Conversation service you can create virtual agents and bots that combine machine learning, natural language understanding, and integrated dialog tools to provide automated customer engagements.

The following image illustrates many uses for the Conversation service.

  ![](./images/usesofconversation.png)

In this lab, you go through a step-by-step process to create your first dialog flow thanks to the easy-to-use graphical environment.


# Objective

In the following lab, you will learn:

+ How to train Watson to understand your users' input with intents and examples
+ How to identify the terms that may vary in your users' input
+ How to create the responses to your user's questions: Dialog Builder
+ How to test and improve your dialog


# Pre-Requisites

+ Get a [Bluemix IBM id](https://bluemix.net)


# Steps

1. [Create a Watson Conversation service](#step-1---create-a-watson-conversation-service)
2. [Create your workspace](#step-2---create-your-workspace)
3. [Work with intents and examples](#step-3---work-with-intents-and-examples)
4. [Work with entities](#step-4---work-with-entities)
5. [Create a dialog](#step-5---create-a-dialog)
6. [Integrate the dialog into a web app](#step-6---integrate-the-dialog-into-a-web-app)


# Step 1 - Create a Watson Conversation service

1. On the Bluemix dashboard, select Catalog from the menu bar.

1. Scroll down to the Services section and click the icon for the Watson Conversation service. The Add Service page opens.

1. Click Create. The service instance is created, and the service dashboard page opens automatically.

1. On the dashboard page, click on the **Launch Tool** to get started. The "Create workspace" page opens.

![](./images/conversation-launchtool.png)


# Step 2 - Create your workspace

One workspace corresponds to one bot — it contains all the configuration information that gives your bot its unique personality. A workspace is a container for all the artifacts that define the behavior of your service.

1. On the "Create workspace" page, click Create.

1. In the **Name** field, type ```Car tutorial```.

1. Choose **English (U.S.)** from one of five languages currently supported.

1. Select **Create**. The new workspace is created and appears as a tile on your dashboard.


# Step 3 - Work with intents and examples

The first thing you’ll see when you open your new workspace is the intents tab. Intents are things that the chat users are looking to do: change passwords, get status updates, make complaints, etc.

What’s really neat about managing intents is that you are actually training the system to understand what is needed without depending on the exact words. You give multiple training examples that correspond to specific actions or requests.

Creating new intents is easy.

1. On the Workspaces page, click the **Car tutorial** workspace tile. The workspace page opens to the Intents tab.

1. On the Intents tab, click **Create new**.

1. In the **Intent name** field, type ```turn_on```. This intent will be used to indicate that the user wants to turn on an appliance such as the radio, windshield wipers, or headlights.

1. Add example utterances that will help Watson recognize the #turn_on intent:

  1. In the **User example** field, type ```I need lights``` and press Enter. The example utterance ```I need lights``` is added to the intent.

  1. Repeat the same process to add the following examples:

      + *Listen to some music*
      + *Play some tunes*
      + *Air on please*
      + *Turn on the headlights*

1. Now that you have added at least 5 examples, click **Done**. The intent is created and appears on the Intents page.

1. Repeat the same process to create a #greeting intent.

 ![](./images/intent-greeting.png)

**Results**

You have now defined two intents (#turn_on and #greeting), along with examples that will train Watson to recognize these intents in user input.

# Step 4 - Work with entities

Entities are the specific pieces of information we want to extract from the user response. You’ll want to group entities that might trigger a similar response in your dialog. Each value can have multiple synonyms, which define different ways that the same value might be specified in user input. When the user's input is received, both intents and entities are identified, and you can use them in the corresponding dialog flow to choose the right response.

Create entities to represent what the user wants to turn on:

1. On the **Car tutorial** workspace page, click the Entities tab.

1. On the Entities tab, click **Create new**.

1. In the **Entity** field, type ```appliance```. The @appliance entity represents an appliance in the car that a user might want to turn on.

1. Define a value for the @appliance entity:

  1. In the **Value** field, type ```music```. This value represents a specific appliance that users might want to turn on.

  1. In the **Synonyms** field, type ```radio```. This indicates that ```radio``` is another way of specifying the same value for the @appliance entity.

  1. Click the plus sign (+) to define additional values for @appliance:

    + ```headlights```, with the synonym ```lights```
    + ```air conditioning```, with the synonym ```air```

  1. Click Done. The @appliance entity is created now appears on the Entities tab.

1. On the Entities tab, click **Create new** to create another entity. Add the entity name ```genre```.

1. Define a value for the @genre entity:

  1. In the **Entity** field, type ```classical```.

  1. In the **Synonyms** field, type ```symphonic```.

1. Click the plus sign (+) to define additional values for @genre:

  + ```rhythm and blues```, with the synonym ```r&b```
  + ```rock```, with the synonym ```pop```

1. Click **Create**. The @genre entity is created and now appears on the Entities tab.

**Results**

You have defined two entities: @appliance (representing an appliance the can turn on) and @genre (representing a genre of music the user can choose). You can now define a dialog that uses intents and entities to choose the correct response.

# Step 5 - Create a dialog

A dialog is a set of conversational nodes that are contained in a workspace. Together the set of nodes makes a dialog tree, on which every branch is a conversation that can be had with a user.

First we need to create a starting node for the dialog:

1. On the **Car tutorial** workspace page, click the Dialog tab.

1. Click **Create**. The dialog is created with a single root node:

  ![](./images/dialog-node-new.png)

1. Specify the condition and response for the starting node of the conversation:

  1. In the **Enter a condition** field, type ```conversation_start```. As you type, a drop-down list appears; select **conversation_start (create new condition)**. This indicates that this node is triggered automatically at the beginning of the conversation.

  1. In the **Enter a response...** field, type ```Welcome to the car demo!``` This is the response that Watson will issue when the specified condition (in this case, the conversation start) is true.

  1. Click the "Anything else" node that was created automatically when you defined the conversation_start node.

  1. In the **Enter a response...** field of the "Anything else" node, type ```I'm sorry, I don't understand. Please try again.``` This is the response that Watson will issue when the user input does not match any other node.

1. Test the conversation:

  1. Click the Try it out ![](./images/dialog-try-new.png) icon. In the chat pane, you should see the response (```Welcome to the car demo```) displayed automatically.

  1. Type any input and press Enter. Because you have not yet defined any other nodes, you should see the response (```I'm sorry, I don't understand. Please try again.```)

  1. Close the chat pane by clicking the X on the top right hand side.

Now we can create dialog branches that handle the defined intents.

1. Create a dialog branch to respond to the #greeting intent. This intent requires only a simple response, so the branch can consist of only a single node.

  1. Click the conversation_start node.

  1. Click the **+** icon on the bottom of the node to create a new root-level node. Because this new node is a peer of the conversation_start node (rather than a subnode), it represents an alternative conversation.

  1. In the **Enter a condition** field, type ```#greeting```. When the drop-down list appears, press Enter to select **#greeting**. This specifies that this node will be triggered by any input that matches the #greeting intent.

  1. In the **Enter a response...** field, specify ```Hi! What can I do for you?```.

  ![](./images/dialog-greeting-new.png)

1. Test the dialog:

  1. Click the ![](./images/dialog-try-new.png) icon to open the chat pane.

  1. Type ```Hello``` and press Enter. The output shows that the #greeting intent is recognized, and the appropriate response appears.

  ![](./images/dialog-greeting-test.png)

1. Create another dialog branch to respond to the #turn_on intent. Because there are multiple possibilities for what the user might want to turn on, this branch requires multiple nodes to represent a more complex conversation. Start by creating the root-level node:

  1. Click the #greeting node, and then the **+** icon on the bottom of the #greeting node to create a new root-level node.

  1. In the **Enter a condition** field, type ```#turn_on```. When the drop-down list appears, press Enter to select **#turn_on**. This specifies that this node will be triggered by any input that matches the #turn_on intent. Leave the **Enter a response...** field blank; the dialog needs more information before it can choose a response.

The #turn_on intent requires additional processing, because the dialog needs to determine what appliance the user wants to turn on. To handle this, we can extend the dialog branch with subnodes:

1. Add a subnode to verify that the user specified a valid appliance to turn on. If the dialog recognizes the #turn_on intent in the user input, the next step is to check the input to make sure the user specified one of the defined values for the @appliance entity. To do this, add a subnode:

  1. Click the **+** icon on the right side of the #turn_on node to create a new subnode.

  1. In the **Enter a condition** field, type ```@appliance```. When the drop-down list appears, press Enter to select **@appliance**. This specifies that this node will be triggered if the user input includes any recognized value for the @appliance entity. Leave the **Enter a response...** field blank; the dialog still needs more information before choosing a response.

  1. In the lower panel  of the #turn_on node, cick the **Jump to...** icon.

  1. Click the @appliance node and then click **Go to condition**. The **Jump to...** link indicates that if the #turn_on node evaluates as true, the dialog flow should pass to the @appliance node without waiting for additional user input. This is necessary because we want the @appliance node to continue evaluating the user's original input rather than waiting for new input.

  ![](./images/tutorial_dialog3-new.png)

1. Now add a peer subnode that will be triggered if the user input did not specify a valid appliance:

  1. Click the **+** icon on the bottom of the @appliance node to create a new peer subnode.

  1. In the **Enter a condition** field, type true. When the drop-down list appears, select **true (create new condition)**. This specifies that if the dialog execution flow reaches this node, it should always evaluate as true. (If the user specified a valid @appliance value, this node will never be reached.)

  1. In the **Enter a response...** field, type ```I'm sorry, I don't know how to do that. I can turn on music, headlights, or air conditioning.```

Now we need to add subnodes to determine the appropriate response when the user has specified a valid appliance:

1. Create a branch of subnodes that handle user requests to play music. Because the user must also specify a genre of music, this branch requires multiple levels of subnodes.

  1. Click the **+** icon on the right side of the @appliance node to create a new subnode. This subnode will be evaluated only if @appliance is true, meaning that the user has specified a valid appliance.

  1. In the **Enter a condition** field, type ```@appliance```. When the drop-down list appears, select **@appliance:music**. This specifies that this node will be triggered if the value of the @appliance entity is music or one of its synonyms, as defined on the Entities tab.

  1. In the **Enter a response...** field, type ```OK! What kind of music would you like to hear?```

  1. In the lower bar of the @appliance node, click the **Jump to...** icon.

  1. Click the @appliance:music node and then click **Go to condition**. The **Jump to...** link indicates that if the @appliance node evaluates as true, the dialog flow should pass to the @appliance:music node without waiting for additional user input.

  ![](./images/tutorial_dialog4-new.png)

  1. Click the **+** icon on the right side of the @appliance:music node to create a new subnode. This subnode will be evaluated only if @appliance is true, and only after the user has responded to the question about genre.

  1. In the **Enter a condition** field, type @genre. When the drop-down list appears, press Enter to select **@genre**. This specifies that this node will be triggered if the user input includes any recognized value for the @genre entity.

  1. In the **Enter a response...** field, type ```OK! Playing @genre```. At run time, the @genre variable will be replaced with the name of the genre specified by the user.

  1. Click the **+** icon on the bottom of the @genre node to create a new peer subnode.

  1. In the **Enter a condition** field, type true. When the drop-down list appears, select **true (create new condition)**. This specifies that if the dialog execution flow reaches this node, it should always evaluate as true. (If the user specified a valid @genre value, this node will never be reached.)

  1. In the **Enter a response...** field, type ```I'm sorry, I don't understand. I can play classical, rhythm and blues, or rock music.```

  ![](./images/tutorial_dialog5-new.png)

1. Test the dialog:

  1. Click the ![](./images/dialog-try-new.png) icon to open the chat pane. Click **Clear** to start a new conversation.

  1. Type ```Play music```. The bot recognizes the #turn_on intent and the @appliance:music entity, and it responds by asking you for a musical genre.

  1. Type the name or a synonym for a valid @genre value. The bot recognizes the @genre entity and responds appropriately.

  1. Type ```Play music``` again, but this time specify an invalid response for the genre. The bot responds by saying it does not understand.

1. Create a subnode to handle user requests to turn on other appliances. Because the other appliances do not require additional information, we can handle these requests with a single node.

  1. Click the **+** icon on the bottom of the @appliance:music node to create a new peer subnode.

  1. In the **Enter a condition** field, type true. When the drop-down list appears, select **true (create new condition)**. This specifies that if the dialog execution flow reaches this node, it should always evaluate as true. In this case, this node will only be reached if the user specified a valid appliance other than music.

  1. In the **Enter a response...** field, type ```OK, turning on the @appliance.```

1. Test the dialog:

  1. Click the ![](./images/dialog-try-new.png)  icon to open the chat pane.

  1. Type ```lights on```. The bot recognizes the #turn_on intent and the @appliance:headlights entity, and it responds with ```OK, turning on the headlights.```

  1. Type ```turn on the air.``` The bot recognizes the #turn_on intent and the @appliance:(air conditioning) entity, and it responds with ```OK, turning on the air conditioning.```

  1. Try variations on all of the supported commands based on the examples and entity synonyms you defined. If the bot fails to recognize the correct intent, you can retrain it directly from the chat window by clicking the incorrect intent and typing the correct intent in the field. (Do not include the # character when you type the intent name.)

  ![](./images/tutorial_dialogtest2.png)


# Step 6 - Integrate the dialog into a web app

You may want to embed this dialog into a web app. This step shows you how to do so using an existing application available in the GitHub repo [Watson simple conversation](https://github.com/watson-developer-cloud/conversation-simple)

## Deploy to Bluemix

1. Use GitHub to clone the repository locally from your terminal using the command

    ```
    git clone https://github.com/watson-developer-cloud/conversation-simple
    ```
    or [download the .zip file](https://github.com/watson-developer-cloud/conversation-simple/archive/master.zip) of the repository and extract the files.

1. Change into the newly created directory with ```cd conversation-simple```.

1. Copy the `.env.example` file to a new file named `.env`.

1. On the Bluemix dashboard, click on your conversation service and click the tab `Service Credentials`. Select `View Credentials` on the first service key and copy the username and password into your `.env` file: Without the quotation marks, paste the `password` and `username` values into the `CONVERSATION_PASSWORD` and `CONVERSATION_USERNAME` variables in the `.env` file.

1. Open the Conversation Service instance by clicking `Launch tool`. If you didn't close the conversation tool, click `Back to workspaces`.

1. Click the actions icon in the upper-right corner of the workspace tile, and then select **View details**.

    ![](./images/conversation-workspace-id.png)

1. Click the ![Copy](./images/copy_icon.png) icon to copy the workspace ID to the clipboard.

1. On the local system, paste the workspace ID into the WORKSPACE_ID variable in the `.env` file. Save and close the file.

1. Connect to Bluemix with the Cloud Foundry command-line tool:
   ```
   cf login
   ```
   When prompted, enter the email and password of your bluemix account.

1. Open the file `manifest.yml` in the local directory `conversation-simple`.
    * Under `applications`, change the `name` to something unique, like `conversation-simple-myapp-[yourName]`.
    * Under `applications-services`, change the service name to the name of your conversation service instance. To quickly check the name of your service, use the `cf services` command to list all services you have created in your bluemix space.

    The following example shows a modified `manifest.yml` file:

    ```
    ---
    declared-services:
     my-conversation-service:
       label: conversation
       plan: free
    applications:
    - name: conversation-simple-myapp-[yourName]
     command: npm start
     path: .
     memory: 256M
     instances: 1
     services:
     - my-conversation-service
     env:
       NPM_CONFIG_PRODUCTION: false
    ```

1. Push the app to Bluemix:

    ```
    cf push
    ```
    Access your app on Bluemix at the URL specified in the command output.

## Test the app locally

You can install and modifiy your app locally and then deploy the modified app to Bluemix.

1. Make sure that you have created the `.env` file as described in previously **Deploy to Bluemix**.

1. Install the demo app package into the local Node.js runtime environment:

    ```bash
    npm install
    ```

1. Start the app:

    ```bash
    npm start
    ```

1. Point your browser to http://localhost:3000 to try out the app.


# Resources

For additional resources pay close attention to the following:

- [Watson Conversation Documentation](http://www.ibm.com/watson/developercloud/doc/conversation/index.shtml)
