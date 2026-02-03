# Setting up a Local AWS Environment with LocalStack and Docker on Windows

## Overview
This guide provides a step-by-step process to emulate AWS services locally using **LocalStack** and **Docker**. This setup allows developers to test cloud-based applications without incurring AWS costs or requiring an internet connection.

## Prerequisites
* Docker Desktop (installed **AND** running)
* Windows PowerShell (run as administrator)

## Installation and Setup
1. Download the lastest LocalStack CLI from the [official releases page](https://github.com/localstack/localstack-cli/releases) and extract the binary to a folder of your choice
2. Run PowerShell as administrator
3. Navigate to the folder where you extracted the binary
	> Tip: You can type `cd` followed by the folder path. Example:
	```powershell
	cd "C:\localstack-folder"
	```
4. **Execute** the binary. Use the command `./localstack.exe`. 
	> **Important**: LocalStack requires the **Docker Engine** to be running. If Docker Desktop is closed, the binary will fail to initialize.

	At this point you should see the list of commands LocalStack accepts.

5. The first thing to setup is the auth-token, which you can do by running
	```powershell
	./localstack.exe auth set-token [your token here]
	```
	If you cannot find your token, it should be in your https://app.localstack.cloud/getting-started
6. Now you only need to run `./localstack.exe start` to get your LocalStack instance up and running.
	> You might be asked to give your browser permission to access the running instance. When doing so you should see the instance indicator turn green on your browser.

7. Environment Variables (Optional But Recommended)
To interact with LocalStack services using the AWS CLI or SDKs, you need to set AWS credential values. If you already have the AWS CLI configured, you can skip this. Otherwise, setting these environment variables ensures that your local commands won't fail due to missing credentials. To set the credentials to dummy values simply run:
	```powershell
	# Run this only if you haven't configured the AWS CLI yet
	$env:AWS_ACCESS_KEY_ID = "test"
	$env:AWS_SECRET_ACCESS_KEY = "test"
	$env:AWS_DEFAULT_REGION = "us-east-1"
	```
	>**Note:** These are mock credentials and do not need to match your actual AWS account.

## Verification 
To verify that LocalStack is running correctly and ready to emulate AWS services, run:
```powershell
./localstack.exe status services
```
You should see a list of AWS services (like S3, Lambda, DynamoDB) marked as `available` or `running`
