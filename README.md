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

name: Custom build and tag...
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
        uses: jppol-idp/tag-and-push-ecr@main
        with:
          source_tag: local-build
          image_name: testing-ecr-tag
          namespace: idp
          image_tags: dev-${{ github.run_number }} test-${{ github.run_number }} ${{ github.sha }}
```
In this example we get a push to `354918371398.dkr.ecr.eu-west-1.amazonaws.com/idp/testing-ecr-tag`



