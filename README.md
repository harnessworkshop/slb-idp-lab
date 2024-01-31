# Workshop Documentation

## Prerequisites
Workshop users must have the following prerequisites in order to successfully complete the workshop:
- Ability to modify code on GitHub
- Accessing the Workshop Account
    - Accept the email invite you receive from the Workshop account.
    - Verify you are in the correct account under Account Settings (your instructor will provide the account name)
    - This step should be unnecessary. But if your email address is associated with other existing Harness accounts and you end up in a different account by mistake, this will take you back to the workshop account.

## Username Selection
Choose a username and use that across the entire lab where you see `<username>`.
- Alpha characters only, no special characters or spaces.

## Lab 1 - Add a Service Component
### Summary
Configure a service component and associate it with a team, and create a dependency.

### Learning Objective(s):
- Defining a service component
- Defining relationships and attributes in a service component
- Browsing different aspects of a component in the UI and YAML

### Part 1: Create a component
1. Login to GitHub.
2. Clone down or access the `slb-idp-lab` repository in the terminal. We will be working on the main branch.
3. Create a new `core-backend` component YAML via the terminal (or GitHub file editor).
4. Copy the contents of the `components/core-backend.yaml`.
5. Create a new file in the `components` directory and title it `core-backend-<username>.yaml`.
    - E.g., My new file location would be `components/core-backend-cassie.yaml`.
6. Create a new `core api` YAML.
7. Copy the contents of the `apis/core-api.yaml`.
8. Create a new file in the `components` directory and title it `core-api-<username>.yaml`.
    - E.g., My new file location would be `apis/core-api-cassie.yaml`.
9. Modify the file fields below in the `components/core-backend.yaml` and the `apis/core-api.yaml` you just made:
    ```yaml
    # Yaml location
    # Original Value: core-backend-<input username>
    # New Value: core-backend-cassie
    metadata:
      name: core-backend-cassie

    # Original Value: - sample - core
    # New Value: - sample - core - cassie
    tags:
      - sample
      - core
      - cassie
    ```
10. Save the changes in your repository.

### Part 2: Register 2 components in Harness
1. Open Harness in a new browser tab.
2. On the left-hand menu, click on “Developer Portal”.
3. On the left-hand sub-menu, click on “Register”.
4. In the URL field, add your `core-api-<username>.yaml` location.
    - Example: [https://github.com/harnessworkshop/slb-idp-lab/blob/main/components/core-backend.yaml](https://github.com/harnessworkshop/slb-idp-lab/blob/main/components/core-backend.yaml)
5. Click Analyze, then Click Import.
6. Upon success, click “View Component”.
7. Repeat steps 3-6 for your `core-backend-<username>.yaml`.

### Part 3: Review components 
With your component from the previous exercise, review various aspects of the component.
- Example component view:
    - With your dependent component open.
    - In the Relations widget: Note that the component is owned by platformteam (group) and is dependent on your first service component.
    - Click on your first component (this will move you into the component).
    - Take note of links, source, etc., that were defined in your component showing up in the UI.
    - Click on the CI/CD, Scorecard, and API tabs.

## Lab 2 - Add CI/CD
### Summary
Configure pipeline relationship.

### Learning Objective(s):
- Link Harness CI/CD results to your registered component
- Documentation for the ADO plugin

### Part 1: Add CI/CD and project details to a component
1. Open your `components/core-backend.yaml` file and add the following under annotations:
    ```yaml
    annotations:
      backstage.io/techdocs-ref: dir:.
      harness.io/project-url: [https://app.harness.io/ng/account/yQvtq8usTqy7F9FkPQgmEA/home/orgs/default/projects/IDP_Workshop/details](https://app.harness.io/ng/account/yQvtq8usTqy7F9FkPQgmEA/home/orgs/default/projects/IDP_Workshop/details)
      harness.io/cd-serviceId: corebackend
    ```
2. Save the file changes.
3. In Harness, open your component and click on the refresh button on the right side of the “About” section.
4. You will see a message that refresh is scheduled. This should take 1-30 seconds.
5. Click on the CI/CD tab.
6. You will see a list of deployments for the associated service.

## Lab 3 - Scorecards

### Summary
Configure scorecard and weights.

### Learning Objective(s)
- Configure a scorecard.

### Part 1: Create a scorecard
1. Go to the "Scorecards" tab under "Admin" and Create New Scorecard.
2. Add the name `<your-username>` as the Name field.
3. Add “platformteam” as the “Owner”.
4. Add “<your-username>” under tags (should auto-populate).
5. Under “Add Checks to Scorecard” on the right, select for following:
    - Spec owner exists
    - Tech Docs exists
    - Deployed within last 7 days
6. Click “Publish Scorecard”.

### Part 2: Review scorecard
1. Navigate to one of your services.
2. Your scorecard should appear with a grade of 75.
3. If more than one scorecard is appearing, give your colleagues the side-eye for misconfiguration of their filters.
4. If the sample scorecard is still present, turn that side-eye inward and request help from the instructor to validate your scorecard’s filters 🙂.
5. Click into the scorecard tab to see what checks passed and failed, detailing out your score.

### Part 3: Change the criteria
Let’s change the grading standards.
1. Navigate to the scorecards under admin, and open your scorecard for editing.
2. Toggle “Adjust Weights” on the right-hand side.
3. Adjust weights to the following:
    - 50 to Spec owner exists
    - 25 to Tech Docs exists
    - 25 to Deploy within last 7 days
4. Click update scorecard.
5. Review your service’s new score.

Congratulations on your passing grade!

---

## Lab 4 - Self Service Workflows - Scaffold a repository

### Summary
Scaffold a repository using self-service workflows.

### Learning Objective(s)
- Understand the configuration behind a self service workflow using a Harness pipeline.

### Part 1: Review the contents of the `onboarding-datascience-template.yaml`
1. Navigate to your repository and open the contents of the `onboarding-datascience-template.yaml`.
2. Take time to understand the file.
3. Open Harness and navigate to this pipeline.

### Part 2: Scaffold a new datascience repository via IDP
1. Go to Harness -> Internal Portal -> Workflows.
2. Under “Workflows” see the Create a cookicutter datascience app workflow.
3. Click on “Choose”.
4. Input the name of the repository you would like to create. (This can be anything).
5. Input the name of a feature branch for the scaffolding to create in the repo (This can be a feature branch name or really, anything. This will be the active working branch when the repo is created).
6. Click on “Next step”.
7. Choose owner “platformteam” from the drop-down.
8. Click on “Create”!
9. You will be directed to the task activity. Find “To view logs please check” line in the logs execution to view the progress of the pipeline.
10. Once the pipeline is completed. Navigate to the `harnessworkshop` organization in GitHub and validate the repository was generated.
11. View the contents of your auto generated data science repository! It’s magic.

## Lab 5 - Self Service Workflows - Kick off Azure DevOps Pipeline

### Summary
Use Harness IDP to run a pipeline in Azure DevOps.

### Learning Objective(s)
- Kick off a pipeline in Azure DevOps via Harness IDP.
- Show how to pass values through to Azure DevOps.

### Part 1: Review the contents of the `ado-webhook-template.yaml`
1. Navigate to your repository and open the contents of the `ado-webhook-template.yaml`.
2. Take time to understand the file.
3. Open Harness and navigate to this pipeline.

### Part 2: Kick off a pipeline in AzureDevOps via IDP
1. Go to Harness -> Internal Portal -> Workflows.
2. Under “Workflows” see the Kick off a pipeline in Azure DevOps workflow.
3. Click on “Choose”.
4. (IMPORTANT) Input “idp-lab” as the name of the project. This is the location of the pipeline we want to kick off in Azure and is being variablized.
5. Click on “Next step”.
6. Choose owner “platformteam” from the drop-down.
7. Click on “Create”.
8. Once the pipeline is completed, navigate to the `harnessworkshop` organization in GitHub and validate the repository was generated.
9. Navigate to this project in Azure to view the pipeline running!
    - Note: Checkout the “Run a one-line script” Job in the pipeline. This echoes a variable which we passed in from Harness. This will be useful when we need to be flexible with what pipeline to target, Terraform variables to pass in, etc.
