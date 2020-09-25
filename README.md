# Demo

## Setup

- Install Node and Docker locally
- Install and configure AWS CLI V2: https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html
- Setup IAM and ECR: https://docs.aws.amazon.com/AmazonECR/latest/userguide/get-set-up-for-amazon-ecr.html

## Push to Container Registry

1. Login to ECR via Docker `aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <account id>.dkr.ecr.us-east-1.amazonaws.com`
2. Create Repository `aws ecr create-repository --repository-name my-test-app --image-scanning-configuration scanOnPush=true --region us-east-1`
3. Build image with `docker build -t my-test-app .`
4. Tag image `docker tag my-test-app:latest <account id>.dkr.ecr.us-east-1.amazonaws.com/my-test-app:latest`
5. Push image `docker push <account id>.dkr.ecr.us-east-1.amazonaws.com/my-test-app:latest`

## Setup Elastic Beanstalk

- Install EB CLI: https://github.com/aws/aws-elastic-beanstalk-cli-setup
- Create Project `eb create`. Set Load Balancer type to network
- Add aws-elasticbeanstalk-ec2-role permissions: https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create_deploy_docker_ecs.html#create_deploy_docker_ecs_role

## Other Docker Commands

- View images `docker images`
- Run image `docker run -p 49160:8080 -d my-test-app`
- View running containers `docker ps`
- View container logs `docker logs <container id>`
- Enter container `docker exec -it <container id> /bin/bash`
