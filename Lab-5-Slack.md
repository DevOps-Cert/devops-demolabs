# Lab 4: Add PagerDuty Integration

# Objective
This lab show how to integrate your toolchain with PagerDuty so people get notified when things go wrong so problems can be fixed faster and reduce downtime.

## Prerequisites
Prior to running this lab, inform the instructor of an email address you would like to use for PagerDuty.  You will need access to this eMail account in order to see notifications in PagerDuty. Check that account to accept the invitation to join PagerDuty.

**Tasks**:
- [Task 1: Add PagerDuty to Toolchain](#task-1-add-pagerduty-to-toolchain)
- [Task 2: Verify PagerDuty works by breaking application build](#task-2-verify-pagerduty-works-by-breaking-application-build)
- [Task 3: Fix application](#task-3-fix-application)

## Task 1: Add PagerDuty to Toolchain
1. On the toolchain's Tool Integrations page, click the add button **+**
2. Select **PagerDuty**
3. On the PagerDuty Configuration page:
   - Enter Nb8ZxY6sAWKxLp1UhA_u as the API access key
   - Enter devopslab as the PagerDuty service name
   - Enter the email address you gave to the instructor as the primary contact email address.  Leave the phone number blank unless you want to receive text messages.

4. Click **Create Integration**

  ![PagerDutySetup](screenshots/PagerDutySetup.jpg)
5. You will need to access the eMail account to accept the PagerDuty invitation.

## Task 2: Add Eclipse Orion Web IDE to Toolchain
We want to modify the application and one way is to use the Web IDE.

1. On the toolchain's Tool Integrations page, click the add button **+**
2. Select **Eclipse Orion Web IDE**.
3. No configuration is needed. so click **Create Integration**.

## Task 3: Verify PagerDuty works by breaking application build
  1. On the toolchain's Tool Integrations page, click the **Eclipse Orion Web IDE** tile. The GitHub repos are automatically loaded in your workspace. The Web IDE workspace is on the cloud.
  2. In the file navigator, expand the catalog-api-toolchain_name repo (if needed).
  3. In the file directory, click manifest.yml to open the file.

  ![WebIDE](screenshots/WebIDE.jpg)
  4. Update the value for memory to 96g. This setting intentionally increases your memory to exceed the quota for your org. Your changes are automatically saved.
  5. Now to Push the changes.  From the Eclipse Orion Web IDE menu, click the **Git** icon.

  ![WebIDEGit](screenshots/WebIDEGit.jpg)

  6. In the Working Directory Changes section, which is in the upper-right corner of the window, make sure that the changed file is selected.  Enter a relevant comment.

  ![WebIDEPush](screenshots/WebIDEPush.jpg)
  7. Click **Commit** to put the changes in the local master branch.
  8. Put these changes in the origin/master branch and click **Push**. Your changes are automatically built and deployed in the pipeline.
  9. Return to your toolchain's Tool Integrations page and click the pipeline tile for the catalog-api microservice to watch the stages run in response to your commit.
  10. The Deploy failed.

  ![WebIDEDeployFailed](screenshots/WebIDEDeployFailed.jpg)
  11. The PagerDuty console (https://ibmdevopslab.pagerduty.com/incidents) shows the incident:

  ![PagerDutyConsole](screenshots/PagerDutyConsole.jpg)
  12. If you entered an email account when you setup the PagerDuty integration, that account will have an email.  The link in the email will allow you to view the incident on PagerDuty.

  ![PagerDutyeMail](screenshots/PagerDutyeMail.jpg)

## Task 4: Fix application

Now to fix the application.
  1. On the toolchain's Tool Integrations page, click the **Eclipse Orion Web IDE** tile.
  2. In the file navigator, expand the catalog-api-toolchain_name repo (if needed).
  3. In the file directory, click manifest.yml to open the file.
  4. Update the value for memory to 96m.
  5. Now to Push the changes.  From the Eclipse Orion Web IDE menu, click the **Git** icon.
  6. In the Working Directory Changes section, which is in the upper-right corner of the window, make sure that the changed file is selected.
  7. Click **Commit** to put the changes in the local master branch.
  8. Put these changes in the origin/master branch and click **Push**. Your changes are automatically built and deployed in the pipeline.
  9. Return to your toolchain's Tool Integrations page and click the pipeline tile for the catalog-api microservice to watch the stages run in response to your commit.
  10. The deploy is successful.  And all the downstream stages run afterwards.

  ![WebIDEDeploySuccess](screenshots/WebIDEDeploySuccess.jpg)