pipeline {
    agent agent
    stages{ 
        stage ('Build') {
            steps {
                sh 'printenv'
               
            }
        }
        stage ('publish ECR') {
            steps {
                withEnv (["AWS_ACCESS_KEY_ID=${env.AWS_ACCESS_KEY_ID}", "AWS_SECRET_ACCESS_KEY=${env.AWS_SECRET_ACCESS_KEY}", "AWS_DEFAULT_REGION=${env.AWS_DEFAULT_REGION}"])
                sh 'docker login --username AWS --password-stdin $(aws ecr-public get-login-password --region us-east-1) public.ecr.aws/w6l1i2y2'
                sh 'docker build -t doxa-ecr .'
                sh 'docker tag doxa-ecr:""$BUILD_ID""'
                sh 'docker push public.ecr.aws/w6l1i2y2/doxa-ecr:""$BUILD_ID""'
            }
        }
    }
}