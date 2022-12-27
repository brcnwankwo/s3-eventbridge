
## Building event-driven applications with Amazon EventBridge and S3.

---

#### What is Event-Driven Architecture?

In event-driven architecture, each component of the application raises an event whenever anything changes. Other components listen and decide what to do with it and how they would like to react.

![](![[Screenshot%202022-12-26%20at%203.26.41%20PM.png]].png)

In this tutorial, I will send an event from AWS S3: the event source, to AWS lambda: the event target using an event rule. I will be configuring events through amazon EventBridge by deploying an AWS SAM template. SAM is an open source framework building serverless applications, which is an extension of CloudFormation.

### Prerequisites:

-   AWS SAM CLI
-   AWS account
-   AWS Access & Secret Key

Go to serverlessland.com and go to code patterns to filter SAM, EventBridge, and S3.

**Step 1: Clone repository and deploy to AWS**

- in the terminal clone the repository:

- `git clone https://github.com/aws-samples/serverless-patterns/ cd serverless-patterns/s3-eventbridge-direct`

	![](![[Screenshot%202022-12-20%20at%206.02.06%20PM.png]].png)

- Run the command `sam deployed --guided` to deploy the S3 bucket that publishes events to EventBridge, and sets up a Lambda function to show how to consume these events via an EventBridge rule. It deploys the the IAM resources required to run the application.

	![](![[Screenshot%202022-12-20%20at%206.07.13%20PM%201.png]].png)

- Choose your Stack Name and Region and then select the default arguments 

	![](![[Screenshot%202022-12-20%20at%206.07.32%20PM%202.png]].png)
	![](![[Screenshot%202022-12-20%20at%206.10.43%20PM.png]].png)
	![](![[Screenshot%202022-12-20%20at%206.11.02%20PM.png]].png)

**Step 2: Create rule in EventBridge**

- In the AWS console go to Amazon EventBridge > Rules and you will see the rules created

	![](![[Screenshot%202022-12-20%20at%206.12.02%20PM.png]].png)
	![](![[Screenshot%202022-12-20%20at%206.12.23%20PM.png]].png)
	![](![[Screenshot%202022-12-20%20at%206.12.40%20PM.png]].png)

**Step 3: Upload photo in S3 Bucket**

- Go to S3 and locate the buckets created

	![](![[Screenshot%202022-12-20%20at%206.13.16%20PM.png]].png)

- Upload image to the S3 bucket

	![](![[Screenshot%202022-12-20%20at%206.15.14%20PM.png]].png)

**Step 4: Create a Lambda function**

- Go to AWS Lambda and see the Lambda function created

	![](![[Screenshot%202022-12-20%20at%206.15.59%20PM.png]].png)

- Go to CloudWatch Logs and view the log created

	![](![[Screenshot%202022-12-20%20at%206.17.09%20PM.png]].png)
	![](![[Screenshot%202022-12-20%20at%206.18.28%20PM.png]].png)
	![](![[Screenshot%202022-12-20%20at%206.18.46%20PM.png]].png)

**Step 5: Create a Rule in EventBridge and view the Logs to see event information**

- Go back to EventBridge and create a rule, event pattern and target

	![](![[Screenshot%202022-12-20%20at%206.19.27%20PM.png]].png)
	![](![[Screenshot%202022-12-20%20at%206.20.15%20PM.png]].png)
	![](![[Screenshot%202022-12-20%20at%206.22.36%20PM.png]].png)
	![](![[Screenshot%202022-12-20%20at%206.23.29%20PM.png]].png)

- Go to CloudWatch logs and view the logs that have been created 

	![](![[Screenshot%202022-12-20%20at%206.27.29%20PM.png]].png)

- Click on the log group and view log streams to view the events 

	![](![[Screenshot%202022-12-20%20at%206.27.41%20PM%201.png]].png)
	![](![[Screenshot%202022-12-20%20at%206.28.07%20PM.png]].png)

**Step 1: Create a Schema in EventBridge**

- Create schema registry and schema name called `user`

	![](![[Screenshot%202022-12-20%20at%207.03.54%20PM.png]].png)
	![](![[Screenshot%202022-12-20%20at%207.04.19%20PM.png]].png)

- Click on Discover from JSON
- Add JSON code and click Discover Schema

```
{"id": 1,
"name": "Name"
"emailAddress": "Email Address"}
```

![](![[Screenshot%202022-12-20%20at%207.07.56%20PM%201.png]].png)

- In EventBridge go to the schema created and click on Download Code Bindings

	![](![[Screenshot%202022-12-20%20at%207.08.20%20PM.png]].png)
	![](![[Screenshot%202022-12-20%20at%207.09.19%20PM.png]].png)

- You can even find the schema in VSCode in the AWS Toolkit under schemas

	![](![[Screenshot%202022-12-20%20at%207.21.00%20PM.png]].png)