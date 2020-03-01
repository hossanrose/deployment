# Flask helloworld
Deploys a python flask app to AWS Elastic Beanstalk

## Application 
Build with web framework Flask. Application responds with a "hello world!" when a GET request is made to /hello
End point : http://concourse-env.eba-37cdi5qb.us-west-2.elasticbeanstalk.com/hello

## Deployment 
Continuous Deployment tool used is concourse as its,
* Easy to setup and configure
* Lightweight and portable
* Provides isolation as it uses containers to run jobs.

Continuous deployment is set in such a way that,
* Application is deployed automatically when an push is made to master branch
* Uses AWS Elastic Beanstalk
* Pipeline code is in deploy directory

### Installation
```
$ wget https://concourse-ci.org/docker-compose.yml
$ docker-compose up -d
```

### Configuration
Set up fly commandline by downloading it from Concourse UI. Use the below commands to setup the pipeline
```
$ fly -t concourse login -c <URL> -u test -p test 
$ fly -t concourse set-pipeline -p EB-Deploy -c flask-eb.yml --var "AWS_ACCESS_KEY_ID=<ID>" --var "AWS_SECRET_ACCESS_KEY=<KEY>" 
```

## Architecture 
Below are the AWS components used by AWS Beanstalk to bring up the application.

- EC2 instance 
- Instance security group 
- Load balancer 
- Load balancer security group
- Auto Scaling group
- Amazon S3 bucket
- Amazon CloudWatch alarms 
- AWS CloudFormation stack 
- Domain name
