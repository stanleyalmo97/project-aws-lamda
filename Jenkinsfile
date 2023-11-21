pipeline {
    agent any
  
   environment {
        aws_Region = 'us-east-1'
    }  
    
    stages {
        stage("Checkout") {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/stanleyalmo97/project-aws-lamda.git']]])
            }
        }

        stage("Package") {
            steps {
                sh "zip -r function.zip ."
                archiveArtifacts artifacts: 'function.zip', fingerprint: true
            }
        }
        
        stage('Deploy to Lambda') {
            steps {
                script {
                    deployLambda([alias: '', artifactLocation: '/var/lib/jenkins/workspace/lambda/', awsAccessKeyId: 'AKIAY72QS32ZDOWHVS5O', awsRegion: 'us-east-1', awsSecretKey: '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', deadLetterQueueArn: '', description: '', environmentConfiguration: [kmsArn: ''], functionName: 'test-lambda', handler: 'lamda_funtion.lambda_handler', memorySize: '', role: 'arn:aws:iam::618107428530:role/service-role/jenkins_lambda-role-a8x2fioa', runtime: 'python3.8', securityGroups: '', subnets: '', timeout: '', updateMode: 'full'])
                }
            }
        }
    }
}
