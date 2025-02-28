# Trigger image update in apps repository

In the IDP app repositories you can create a file describing images, that you want to update 
to the latest version by ECR lookup of image tag. You can also provide filter on tag names. 

This action can trigger the process in the apps repository. 

You will need an application id and secret provided by IDP team. 

# Example
If you just want to build a Dockerfile in the current folder of the action, tag it 
and push it to ECR (optionally creating the repository if it does not exist), you should 
do something like

```yaml

name: Update image tags
on:
  workflow_dispatch:
jobs:
  build_and_push:
    runs-on: ubuntu-24.04
    permissions: write-all
    strategy:
      fail-fast: false
    steps:
      - name: Push 
        id: push
        uses: jppol-idp/trigger-image-update@main
        with:
          application_id: {{ var.IDP_DEPLOY_TRIGGER }}
          application_secret: {{ secrets.IDP_DEPLOY_TRIGGER_KEY }}
          apps_repository: apps-koa
```

Here we use a variable for application id and a secret for the key. These should of course be 
stored in the repo using the action.


