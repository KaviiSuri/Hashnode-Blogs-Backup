## How to setup CD for AWS Elastic Beanstalk using CodePipeline?

## Introduction
So, Now you have your code running on AWS. It's secure and cheap, but you still have to upload your code in zip files. How archaic😱!! Let's fix this in this article using another awesome AWS Service called the CodePipeline. This is gonna be a short one guys.

> This article is a sequel to the previous one called  [How to setup a https server in elastic beanstalk](https://kavii.hashnode.dev/how-to setup-a-https-server-in-elastic-beanstalk-the-cheap-way). It's not required to read the previous one, but I would recommend doing so before reading this. 

## What is Code Pipeline?
It is an AWS Service that provides fully managed, continous devlivery that helps you automate the release pipelines for fast and reliable application and infrastructure.
You can automate various phases like 
- Build
- Test
- Deploy
and this automation will run every time there is a code change.

It supports various source code sources, we'll be using github but there is very little difference in how to use any other service if you need to.

## How to Setup CD
Go to code pipeline option in your console and press "Create New Pipeline". 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630381331383/FGHTgUZiZ.png)

Enter the name and leave everything as default. Click "Next"

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630381374560/KEF2botrA.png)

In the source stage, select the provider and fill in the details. We'll be using Github (Version 2) here.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630381449076/AEzwehIaS.png)

If you require a build stage, configure this step. We'll be skipping this stage.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630381531434/T9VLqpwx3.png)

In the deploy stage, select AWS Elastic Beanstalk and fill other details.
Click "Next" and review everything. 

## Conclusion

Once you submit, your pipeline will be active. Now, as soon as you push code to github, it'll reflect in your deployment very soon.

### Readme Badges
If you need github readme badges, refer to [this article] (https://medium.com/swlh/aws-ci-cd-dynamic-build-badge-display-on-github-1e9a3b76db5a) for how to set it up. You can also use  [this npm library](https://www.npmjs.com/package/cdk-pipeline-status)  for monitoring the status.