# Deployment URL

https://portal.azure.com/#@dhananjaysharma207outlook.onmicrosoft.com/resource/subscriptions/355045d5-ce60-484e-8ca3-8fe243d73abc/resourceGroups/proj1/providers/Microsoft.BotService/botServices/healbot3/overview




# Output

![Screenshot (8944)](https://user-images.githubusercontent.com/92742019/150644504-b8b122c4-54c4-4123-b632-5fefef617743.png)
![Screenshot (8945)](https://user-images.githubusercontent.com/92742019/150644549-e7e7d245-56f7-46b5-bf59-77be42abbe3f.png)
![Screenshot (8946)](https://user-images.githubusercontent.com/92742019/150644563-35b86719-e336-43b1-8de1-24f8615c775b.png)
![Screenshot (8947)](https://user-images.githubusercontent.com/92742019/150644617-6dc87193-9ae6-4eac-8082-535c4c750568.png)
![Screenshot (8948)](https://user-images.githubusercontent.com/92742019/150644627-7170b83b-f2c4-401c-9f33-7a431952a0e0.png)
![Screenshot (8949)](https://user-images.githubusercontent.com/92742019/150644641-147ac911-3a5a-4ad9-bd4b-d03beedb857f.png)
![Screenshot (8950)](https://user-images.githubusercontent.com/92742019/150644650-6631bc1f-abf0-4dfa-950e-13f42fcf173d.png)
![Screenshot (8951)](https://user-images.githubusercontent.com/92742019/150644682-f5a11395-60c9-44f4-8c2d-d4ccf185d939.png)
![Screenshot (8952)](https://user-images.githubusercontent.com/92742019/150644695-220d4f59-f9ab-4833-9bae-9342580f1d0b.png)
![Screenshot (8953)](https://user-images.githubusercontent.com/92742019/150644723-74655835-e5ff-4628-80c9-d5793131848f.png)

# Project URL

https://github.com/Dhananjaysharma207/Chat-assistant-bot-for-people

# Demo Url

https://sites.google.com/akgec.ac.in/dhananjaycovidbot/home?authuser=1

# QnA Maker

Bot Framework v4 QnA Maker bot sample. This sample shows how to integrate Multiturn and Active learning in a QnA Maker bot with ASP.Net Core-2. Click [here][72] to know more about using follow-up prompts to create multiturn conversation. To know more about how to enable and use active learning, click [here][71].

This bot has been created using [Bot Framework](https://dev.botframework.com), it shows how to create a bot that uses the [QnA Maker Cognitive AI](https://www.qnamaker.ai) service.

The [QnA Maker Service](https://www.qnamaker.ai) enables you to build, train and publish a simple question and answer bot based on FAQ URLs, structured documents or editorial content in minutes. In this sample, we demonstrate how to use the QnA Maker service to answer questions based on a FAQ text file used as input.

## Concepts introduced in this sample
The [QnA Maker Service][7] enables you to build, train and publish a simple question and answer bot based on FAQ URLs, structured documents or editorial content in minutes.
In this sample, we demonstrate 
-.how to use the Active Learning to generate suggestions for knowledge base.
-.how to use the Multiturn experience for the knowledge base .

# Prerequisites
`- Follow instructions` [here](https://docs.microsoft.com/en-us/azure/cognitive-services/qnamaker/how-to/set-up-qnamaker-service-azure) to create a QnA Maker service.
- Follow instructions [here](https://docs.microsoft.com/en-us/azure/cognitive-services/qnamaker/how-to/multiturn-conversation) to create multiturn experience.
- Follow instructions [here](https://docs.microsoft.com/en-us/azure/cognitive-services/qnamaker/quickstarts/create-publish-knowledge-base) to import and publish your newly created QnA Maker service.
- Update [appsettings.json](appsettings.json) with your kbid (KnowledgeBase Id), endpointKey and endpointHost. QnA knowledge base setup and application configuration steps can be found [here](https://aka.ms/qna-instructions).
- (Optional) Follow instructions [here](https://github.com/Microsoft/botbuilder-tools/tree/master/packages/QnAMaker) to set up the
QnA Maker CLI to deploy the model.


### Create a QnAMaker Application to enable QnA Knowledge Bases

QnA knowledge base setup and application configuration steps can be found [here](https://aka.ms/qna-instructions).

# Configure Cognitive Service Model
- Create a Knowledge Base in QnAMaker Portal.
- Import "smartLightFAQ.tsv" file, in QnAMaker Portal.
- Save and Train the model.
- Create Bot from Publish page.
- Test bot with Web Chat.
- Capture values of settings like"QnAAuthKey" from 
- "Configuration" page of created bot, in Azure Portal.
- Updated appsettings.json with values as needed.
- Use value of "QnAAuthKey" for setting "QnAEndpointKey".
- Capture KnowledgeBase Id, HostName and EndpointKey current published app 

# Try Active Learning
- Once your QnA Maker service is up and you have published the sample KB, try the following queries to trigger the Train API on the bot.
- Sample query: "light"
- You can observe that, Multiple answers are returned with high score.

# Try Multi-turn prompt
- Once your QnA Maker service is up and you have published the sample KB, try the following queries to trigger the Train API on the bot.
- Sample query: "won't turn on"
- You can notice a prompt, included as part of  answer to query.

## To try this sample

- Clone the repository

    ```bash
    git clone https://github.com/Microsoft/botbuilder-samples.git
    ```

- In a terminal, navigate to `samples/csharp_dotnetcore/49.qnamaker-all-features`
- Run the bot from a terminal or from Visual Studio, choose option A or B.

  A) From a terminal

  ```bash
  # run the bot
  dotnet run
  ```

  B) Or from Visual Studio

  - Launch Visual Studio
  - File -> Open -> Project/Solution
  - Navigate to `samples/csharp_dotnetcore/49.qnamaker-all-features` folder
  - Select `QnABot.csproj` file
  - Press `F5` to run the project

##### Microsoft Teams channel group chat fix
- Goto `Bot/QnABot.cs`
- Add References
    ~~~
    using Microsoft.Bot.Connector;
    using System.Text.RegularExpressions;
    ~~~
- Modify `OnTurnAsync` function as:
    ~~~
    public override async Task OnTurnAsync(ITurnContext turnContext, CancellationToken cancellationToken = default)
        {
            // Teams group chat
            if (turnContext.Activity.ChannelId.Equals(Channels.Msteams))
            {
                turnContext.Activity.Text = turnContext.Activity.RemoveRecipientMention();
            }
            
            await base.OnTurnAsync(turnContext, cancellationToken);

            // Save any state changes that might have occurred during the turn.
            await ConversationState.SaveChangesAsync(turnContext, false, cancellationToken);
            await UserState.SaveChangesAsync(turnContext, false, cancellationToken);
        }
    ~~~

## Testing the bot using Bot Framework Emulator

[Bot Framework Emulator](https://github.com/microsoft/botframework-emulator) is a desktop application that allows bot developers to test and debug their bots on localhost or running remotely through a tunnel.

- Install the Bot Framework Emulator version 4.3.0 or greater from [here](https://github.com/Microsoft/BotFramework-Emulator/releases)

### Connect to the bot using Bot Framework Emulator

- Launch Bot Framework Emulator
- File -> Open Bot
- Enter a Bot URL of `http://localhost:3978/api/messages`

# Deploy the bot to Azure
See [Deploy your C# bot to Azure][50] for instructions.

The deployment process assumes you have an account on Microsoft Azure and are able to log into the [Microsoft Azure Portal][60].

If you are new to Microsoft Azure, please refer to [Getting started with Azure][70] for guidance on how to get started on Azure.

# Further reading
* [Active learning Documentation][al#1]
* [Bot Framework Documentation][80]
* [Bot Basics][90]
* [Azure Bot Service Introduction][100]
* [Azure Bot Service Documentation][110]
* [msbot CLI][130]
* [Azure Portal][140]

[1]: https://dev.botframework.com
[2]: https://docs.microsoft.com/en-us/visualstudio/releasenotes/vs2017-relnotes
[3]: https://dotnet.microsoft.com/download/dotnet-core/3.1
[4]: https://docs.microsoft.com/en-us/azure/bot-service/bot-service-overview-introduction?view=azure-bot-service-4.0
[5]: https://github.com/microsoft/botframework-emulator
[6]: https://aka.ms/botframeworkemulator
[7]: https://www.qnamaker.ai

[50]: https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-howto-deploy-azure?view=azure-bot-service-4.0
[60]: https://portal.azure.com
[70]: https://azure.microsoft.com/get-started/
[80]: https://docs.botframework.com
[90]: https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0
[100]: https://docs.microsoft.com/en-us/azure/bot-service/bot-service-overview-introduction?view=azure-bot-service-4.0
[110]: https://docs.microsoft.com/en-us/azure/bot-service/?view=azure-bot-service-4.0
[120]: https://docs.microsoft.com/en-us/cli/azure/?view=azure-cli-latest
[130]: https://github.com/Microsoft/botbuilder-tools/tree/master/packages/MSBot
[140]: https://portal.azure.com
[150]: https://www.luis.ai

[71]: https://docs.microsoft.com/en-us/azure/cognitive-services/qnamaker/how-to/improve-knowledge-base
[72]: https://docs.microsoft.com/en-us/azure/cognitive-services/qnamaker/how-to/multiturn-conversation
https://dhananjaysharma207.github.io/Chat-assistant-bot-for-people/ tap here for a quick recap of my project.

