# CircleCI - Grace Hopper Jeopardy

## Run locally

Run the following:

    npm install
    npm run webpack

Then open index.html in your browser.

## Deploy on AWS

This application can be deployed to Amazon EC2 using AWS CloudFormation and AWS CodeDeploy.  It can be used as an example application in a workshop, with multiple stacks in the same account.

Create shared resources (create once):
```
aws cloudformation deploy --stack-name ghc-workshop-shared-resources --template-file cfn/shared_resources.yml --capabilities CAPABILITY_NAMED_IAM --parameter-overrides WorkshopName="ghc-workshop"
```

Create website resources (can create multiple stacks for a workshop):
```
aws cloudformation deploy --stack-name ghc-workshop-application-1 --template-file cfn/application.yml --parameter-overrides SharedResourceStack="ghc-workshop-shared-resources"
```

Once the deployment completes, go to the application URL:
```
aws cloudformation describe-stacks --stack-name ghc-workshop-application-1 --query 'Stacks[0].Outputs[?OutputKey==`Url`].OutputValue' --output text
```

Cleanup:
```
Delete Stacks:

aws cloudformation delete-stack --stack-name ghc-workshop-shared-resources

aws cloudformation delete-stack --stack-name ghc-workshop-application-1
```

## Credits
* Based on [React Trivia](https://github.com/ccoenraets/react-trivia)
* Grace Hopper clip art by [gingercoons](https://openclipart.org/detail/137533/grace-hopper)

