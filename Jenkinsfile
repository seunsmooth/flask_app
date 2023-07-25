pipeline {
  agent any
    stages{ 
        stage ('Build') {
            steps {
                sh 'printenv'
               
            }
        }
        stage ('publish ECR') {
            steps {
              withEnv (["AWS_ACCESS_KEY_ID=${env.AWS_ACCESS_KEY_ID}", "AWS_SECRET_ACCESS_KEY=${env.AWS_SECRET_ACCESS_KEY}", "AWS_DEFAULT_REGION=${env.AWS_DEFAULT_REGION}"]) {
                sh '/usr/local/bin/docker login -u AWS -p $(/usr/local/bin/aws ecr-public get-login-password --region us-east-1) public.ecr.aws/w6l1i2y2'
                sh '/usr/local/bin/docker build -t doxa-ecr .'
                sh '/usr/local/bin/docker tag doxa-ecr:latest public.ecr.aws/w6l1i2y2/doxa-ecr:""$BUILD_ID""'
                sh '/usr/local/bin/docker push public.ecr.aws/w6l1i2y2/doxa-ecr:""$BUILD_ID""'
            }
            }
        }
    }
}