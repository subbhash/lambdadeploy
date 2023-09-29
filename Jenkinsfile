pipeline {

    agent {

        label 'test' 

    }

    environment {

        AWS_REGION = 'ap-southeast-2'

        AWS_ACCOUNT_ID = '456464382094'

        LAMBDA_FUNCTION_NAME = 'my-function'

        ECS_CLUSTER = 'default-cluster'

        ECS_SERVICE = 'Jenkins-JenkinsService-NnQOe2Ia5QuL'

        TASK_DEFINITION = 'jenkins-task:ACTIVE'

    }

    stages {

        stage('Deploy to ECS') {

            steps {

                script {

                    sh 'aws configure set aws_access_key_id $AWS_ACCESS_KEY_ID'

                    sh 'aws configure set aws_secret_access_key $AWS_SECRET_ACCESS_KEY'

                    sh 'aws configure set default.region $AWS_REGION'

 

                    sh 'aws ecs update-service --cluster $ECS_CLUSTER --service $ECS_SERVICE --task-definition $TASK_DEFINITION'

 

                    echo 'ECS service updated!'

                }

            }

        }

 

        stage('Update Lambda Function') {

            steps {

                script {

                    sh "aws lambda update-function-code --function-name $LAMBDA_FUNCTION_NAME --image-uri $ECR_REPO_URI:$IMAGE_TAG"

                    

                    echo 'Lambda function updated!'

                }

            }

        }

    }

}
