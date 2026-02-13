# Lab 3 Submission
## Task 1: First GitHub Actions Workflow

#### Link to the successful workflow run: 
[Link](https://github.com/arinapetukhova/DevOps-Intro/actions/runs/21980663308)

### Key Concepts Learned:
GitHub Actions is an automation tool triggered by repository events. **Jobs** are the main execution units that run independently; this workflow contained a single job named "Explore-GitHub-Actions". **Steps** are individual tasks within a job, such as echo commands or the actions/checkout action. **Runners** are the virtual machines that execute workflows; this job ran on a GitHub-hosted Linux runner. **Triggers** are events that initiate workflows; this workflow was configured to run on push events.

### What Caused This Run to Trigger
The workflow was triggered by a push event to a new branch feature/lab3. When the branch was created locally and pushed to the remote repository, GitHub detected the push and automatically started the workflow.

### Analysis of Workflow Execution Process
First, GitHub set up a Linux runner with version 2.331.0. The actions/checkout@v5 action was downloaded using a specific hash to ensure version consistency.

The workflow then executed several echo steps that printed information about the trigger event, runner environment, and branch name. Next, the checkout action cloned the repository onto the runner. Authentication was configured using GITHUB_TOKEN, and the exact commit from the feature/lab3 branch was checked out. A directory listing confirmed the presence of project files (app, labs, lectures, README.md, and test.txt).

After all steps completed successfully, post-job cleanup was performed. Git configuration settings were removed, authentication headers were unset, and the runner was terminated. This demonstrates how GitHub Actions provides a temporary, isolated, and secure environment for each workflow execution.

#### Link to the successful workflow run: 

## Task 2: Manual Trigger + System Information
