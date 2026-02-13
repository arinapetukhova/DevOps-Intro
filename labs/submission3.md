# Lab 3 Submission
## Task 1: First GitHub Actions Workflow

### Link to the successful workflow run: 
[Link](https://github.com/arinapetukhova/DevOps-Intro/actions/runs/21980663308)

### Key Concepts Learned:
GitHub Actions is an automation tool triggered by repository events. **Jobs** are the main execution units that run independently; this workflow contained a single job named "Explore-GitHub-Actions". **Steps** are individual tasks within a job, such as echo commands or the actions/checkout action. **Runners** are the virtual machines that execute workflows; this job ran on a GitHub-hosted Linux runner. **Triggers** are events that initiate workflows; this workflow was configured to run on push events.

### What Caused This Run to Trigger
The workflow was triggered by a push event to a new branch feature/lab3. When the branch was created locally and pushed to the remote repository, GitHub detected the push and automatically started the workflow.

### Analysis of Workflow Execution Process
First, GitHub set up a Linux runner with version 2.331.0. The actions/checkout@v5 action was downloaded using a specific hash to ensure version consistency.

The workflow then executed several echo steps that printed information about the trigger event, runner environment, and branch name. Next, the checkout action cloned the repository onto the runner. Authentication was configured using GITHUB_TOKEN, and the exact commit from the feature/lab3 branch was checked out. A directory listing confirmed the presence of project files (app, labs, lectures, README.md, and test.txt).

After all steps completed successfully, post-job cleanup was performed. Git configuration settings were removed, authentication headers were unset, and the runner was terminated. This demonstrates how GitHub Actions provides a temporary, isolated, and secure environment for each workflow execution.

## Task 2: Manual Trigger + System Information

### Link to the manual workflow run: 
[Link](https://github.com/arinapetukhova/DevOps-Intro/actions/runs/21989980188)

### Changes made to the workflow file:
`workflow_dispatch` was added:
```
on: 
  push:
  workflow_dispatch:
```

System information collection step was added, as well:
```
- name: Gather system information
  run: |
    echo "## System Information" 
    echo "### Operating System Details"
    cat /etc/os-release
    echo ""
    echo "### CPU Information"
    lscpu | grep "Model name\|CPU(s)"
    echo ""
    echo "### Memory Information"
    free -h
    echo ""
    echo "### Disk Information"
    df -h
    echo ""
    echo "### Kernel Version"
    uname -a
    echo ""
    echo "### Who am I"
    whoami
    echo ""
    echo "### Current Directory"
    pwd
    echo ""
    echo "### Environment Variables"
    env | sort
```

### Gathered system information from runner:
The runner is an Ubuntu 24.04.3 LTS virtual machine hosted on Azure, running Linux kernel 6.14.0-1017-azure. Hardware includes an AMD EPYC 7763 processor with 4 CPU cores, 15GB RAM (plus 3GB of swap space), and 145GB storage with 92GB free. The repository is cloned to /home/runner/work/DevOps-Intro/DevOps-Intro under the "runner" user account.

### Manual vs Automatic Workflow Triggers:
The last run was triggered manually using `workflow_dispatch`. Automatic push triggers run immediately after code changes, ideal for continuous integration. Manual triggers provide on-demand control for testing and debugging. Both trigger types execute the same steps.

### Analysis of runner environment and capabilities:
The runner gives user a clean, separate, and temporary setup with many tools already installed, like different versions of Java, Go, Android SDK, and .NET. It is short-lived — a new one is created for each job and removed afterward, so no leftover files affect future runs. GitHub-hosted runners always have the same hardware and software setup, and security is handled automatically — login info and secrets are erased when the job finishes. The environment is built specifically for automated testing and integration tasks.