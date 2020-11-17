# Gitlab DevOps

Our project uses Gitlab CI/CD pipelines to test, build, and deploy our code. With Gitlab, we are able to list the deployed environments in the **Operations/Environments** page for each of our three development repositories. In this view, you can see what code is in **stage** and what code is in **prod**.

We use these two environments to test our code \(in **stage**\) and to deploy our code so that it can reach users \(in **prod**\).

## Set up runners

Each of the gitlab pipelines requires different dependencies, so there are tags on these jobs to indicate what kind of setup is required.

### docker

Requires having [docker](https://docs.docker.com/get-docker/) installed locally.

### unity

Requires having [Unity](https://unity3d.com/get-unity/download) installed locally.

### brew-installed

Requires having [brew](https://brew.sh) installed locally.



