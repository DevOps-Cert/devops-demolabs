# Integrate Slack

## Objective

Bluemix DevOps services include toolchains working together to support your development and deployment tasks. The integrations across a toolchain help ease the workflows between the tools so they work in synergy.  This lab demonstrates how to set-up and use Bluemix toolchains with Slack to make your move to DevOps easier.  **Note:** Toolchains are currently available in the US South region only and the instructions in this lab are written for the US South region.

This lab uses the simple toolchain for the Orders API microservice.

### Teaming

Software development is a team activity.  The lab scenario shows how Bluemix Continuous Delivery tool integrations can be used to alerts teams when activities, such as builds or deployments, occur.

## Tasks
- [Task 1: Integrate Slack into Toolchain](#task-1-integrate-slack-into-toolchain)
- [Task 2: Test Slack Integration](#task-2-test-slack-integration)
- [Task 3: Break the application build](#task-3-break-the-application-build)
- [Task 4: Fix application](#task-4-fix-application)

## Task 1: Integrate Slack into Toolchain

The visual display of the Delivery Pipeline is great if you want to watch it.  But if you don't want to watch or if you did not even start the build, how do you get notified of events that you are interested in?  One way is Slack.  Slack provides real-time messaging for team communications. You can integrate Slack with your Bluemix DevOps Services project so that notifications about build results from your Delivery Pipeline are posted on a Slack channel.

1. If you are not on the Toolchains page (if you don't see a button called _Create a Toolchain_), click on the **Bluemix menu bar** in the upper left corner.
![BluemixMenuBar](screenshots/BluemixMenuBar.png)
and click on **Services** then **DevOps**.
2. Click <b>simple-order-toolchain-<i>timestamp</i></b>.
3. On the <b>simple-order-toolchain-<i>timestamp</i></b> Toolchain page, click **Add a Tool**.
4. Select **Slack**
5. On the Slack Configuration page:
   - Enter the following all as one string as the Slack webhook. This is also available for copying and pasting at:
   [http://ibm.biz/SlackWebHook](http://ibm.biz/SlackWebHook).
```
  https://hooks.slack.com/services/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
```

   - Enter **#demolab_devops** as the Slack channel.
   - Enter **BluemixDevOpsLab** as the Slack team name.
  ![CreateSlack](screenshots/CreateDevOpsSlack.png)

6. Click **Create Integration**
7. The integration with Slack is added.
![SlackIntegrationCreated](screenshots/SlackIntegrationCreated.png)
8. Switch to the browser tab that has Slack open.  If the tab is closed:
  - Open a new browser tab
  - Go to the following URL to go to the Slack team
    [https://bluemixdevopslab.slack.com](https://bluemixdevopslab.slack.com)
  - If asked, enter the following information:
    - Email address: **BluemixDevOps@gmail.com**
    - Password: **bluemix4me**
    and click **Sign in**.
9. Slack notifies us that the integration was added.
![SlackIntegrationSlackNotice](screenshots/SlackIntegrationSlackNotice.png)

## Task 2: Test Slack Integration

Looking at the _demolab_devops_ Slack channel, we might see that other team members have been busy.  Let's see what happens when we initiate a build.

1. Switch to the browser tab displaying the Bluemix console. It should be displaying the <b>simple-order-toolchain-<i>timestamp</i></b> Toolchain page.  If not, click on the Bluemix menu bar in the upper left corner, click on Services then DevOps.  Click on Toolchains.  Then click on <b>simple-order-toolchain-<i>timestamp</i></b>.
2. Click on the **Delivery Pipeline** tile for the orders-api-toolchain-demo Delivery Pipeline.
![SimpleOrdersAPIClickDeliveryPipeline](screenshots/SimpleOrdersAPIClickDeliveryPipeline.png)
3. Start an application build by clicking on the _BUILD_ stage **Run Stage** icon.
![SimpleOrdersAPIClickRunBuildStage](screenshots/SimpleOrdersAPIClickRunBuildStage.png)
4. Switching to the Slack browser tab, the Slack bluemixdevopslab channel displays the progress of this activity.
![SimpleOrdersAPISlackBuildStageStarted](screenshots/SimpleOrdersAPISlackBuildStageStarted.png)
5. And the completion.
![SimpleOrdersAPISlackBuildStageFinished](screenshots/SimpleOrdersAPISlackBuildStageFinished.png)
6. Through the Bluemix Continuous Delivery integration with Slack, teams get notified of events in the Delivery Pipeline.
7. Switch to the browser tab displaying the Bluemix console.  Click the blue arrow in the upper left hand corner to return to the Toolchain.

## Task 3: Break the application build

Let's see what happens when the application build is broken.

1. On the <b>simple-order-toolchain-<i>timestamp</i></b> Toolchain page, click the **Eclipse Orion Web IDE** tile.
2. In the file directory, click manifest.yml to open the file.
![OrderAPIOrionManifest](screenshots/OrderAPIOrionManifest.png)
3. Update the value for memory to 96G. This setting intentionally increases your memory to exceed the quota for your org. Your changes are automatically saved.
![OrderAPIOrionManifestOld](screenshots/OrderAPIOrionManifestOld.png)
4. From the Eclipse Orion Web IDE menu, click the **Git** icon.
![OrderAPIOrionGit](screenshots/OrderAPIOrionGit.png)
5. Enter a relevant comment and click **Commit** to push the changes in the local master branch.
![OrderAPIOrionGitCommit](screenshots/OrderAPIOrionGitCommit.png)
6. Click **Push** to put the changes into GitHub.
![OrderAPIOrionGitPush](screenshots/OrderAPIOrionGitPush.png)
7. Your changes are automatically built and deployed in the pipeline.
8. Click the blue arrow in the upper left hand corner to return to the Toolchain.
![OrderAPIOrionReturn](screenshots/OrderAPIOrionReturn.png)
9. Click the tile for the _order-api-toolchain-lab<i>timestamp</i>_ Delivery Pipeline. Our change caused the deployment to fail.
![OrderAPIDevDeployFailed](screenshots/OrderAPIDevDeployFailed.png)
3. Switch to the Slack browser tab, Slack also notifies the team about the Deployment failure.
![SimpleOrdersAPISlackDeployFailed](screenshots/SimpleOrdersAPISlackDeployFailed.png)
4. In Slack, there are a few links to go to the Stage, Job Input or Job. Click the **Failed** link for the Blue/Green Deploy job.
![SimpleOrdersAPISlackDeployFailedLinks](screenshots/SimpleOrdersAPISlackDeployFailedLinks.png)
0. Looking at the _Blue/Green Deploy_ Job log (and scrolling down), we can see why it failed.
![OrderAPIDevDeployFailedLog](screenshots/OrderAPIDevDeployFailedLog.png)
Return to the Toolchain by clicking on the vertical ellipsis on the upper right of the Bluemix console page and selecting **View Toolchain**.
![SimpleOrdersAPIClickToolchain](screenshots/SimpleOrdersAPIClickToolchain.png)

## Task 4: Fix application

Now to fix the application.
1. On the <b>simple-order-toolchain-<i>timestamp</i></b> Toolchain, click the **Eclipse Orion Web IDE** tile.
2. In the file directory, click manifest.yml to open the file.
3. Update the value for memory to 96M.
4. Now to Commit and Push the changes.  From the Eclipse Orion Web IDE menu, click the **Git** icon.
5. Click **Commit** to put the changes in the local master branch (enter a relevant Commit comment).
6. Click **Push**. Your changes are automatically built and deployed in the pipeline.
7. Return to Toolchain page and click the Delivery Pipeline tile to watch the stages run in response to your code changes.
8. You could also display the Slack browser tab to display the Delivery Pipeline progress.
8. The deploy is successful and all the downstream stages run afterwards.
9. The Delivery Pipeline shows the Git URL and Git commit link.
![SimpleOrdersAPIGitLink.png](screenshots/SimpleOrdersAPIGitLink.png)
0. Click the Git commit link to show the changes that were committed that caused the Delivery Pipeline to execute.
![SimpleOrdersAPIGITIssue](screenshots/SimpleOrdersAPIGITIssue.png)
1. Return to the Toolchains page. 
