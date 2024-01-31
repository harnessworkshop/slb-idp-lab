# Workshop Documentation

## Prerequisites
Workshop users must have the following prerequisites in order to successfully complete the workshop:

- Ability to modify code on GitHub
- Access to the Workshop Account
    - Accept the email invite you receive from the Workshop account.
    - Verify you are in the correct account under Account Settings (your instructor will provide the account name)

Username Selection:
- Choose a username and use that across the entire lab where you see `<username>`
    - Alpha characters only, no special characters or spaces

## Lab 1 - Add a Service Component
### Summary
Configure a service component and associate it with a team, and create a dependency.

### Learning Objectives:
- Defining a service component
- Defining relationships and attributes in a service component
- Browsing different aspects of a component in the UI and YAML

### Part 1: Create a component
1. Login to GitHub
2. Clone down or access the `slb-idp-lab` repository in the terminal. We will be working on the main branch.
3. Create a new `core-backend` component YAML via the terminal (or GitHub file editor).
4. Copy the contents of the `components/core-backend.yaml`.
5. Create a new file in the `components` directory and title it `core-backend-<username>.yaml`.
6. Create a new `core api` YAML.
7. Copy the contents of the `apis/core-api.yaml`.
8. Create a new file in the `components` directory and title it `core-api-<username>.yaml`.
9. Modify the file fields below in the `components/core-backend.yaml` and the `apis/core-api.yaml` you just made.
   - **YAML location**:
       - Original Value: `core-backend-<input username>`
       - New Value: `core-backend-cassie`
   - **tags**:
       - Original Value: `- sample - core`
       - New Value: `- sample - core - cassie`
10. Save the changes in your repository.

### Part 2a: Register 2 components in Harness
1. Open Harness in a new browser tab.
2. On the left-hand menu click on “Developer Portal”.
3. On the left-hand sub-menu, click on “Register”.
4. In the URL field, add your `core-api-<username>.yaml` location.
    - Example: `https://github.com/harnessworkshop/slb-idp-lab/blob/main/components/core-backend.yaml`
5. Click Analyze, then Click Import.
6. Upon success, click “View Component”.
7. Repeat steps 3-6 for your `core-backend-<username>.yaml`.

### Part 4: Review components
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

### Learning Objectives:
- Link Harness CI/CD results to your registered component
- Documentation for the ADO plugin

### Part 1: Add CI/CD and project details to a component
1. Open your `components/core-backend.yaml` file and add the following under annotations:
   ```yaml
   annotations:
     backstage.io/techdocs-ref: dir:.
     harness.io/project-url: https://app.harness.io/ng/account/yQvtq8usTqy7F9FkPQgmEA/home/orgs/default/projects/IDP_Workshop/details
     harness.io/cd-serviceId: corebackend
