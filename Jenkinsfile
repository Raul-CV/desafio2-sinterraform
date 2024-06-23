pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'eu-west-2'
        LAMBDA_FUNCTION_NAME = 'new_func'
        ZIP_FILE_NAME = 'lambda.zip'
    }

    stages {
        // stage('Checkout') {
        //     steps {
        //         git branch: 'main', url: 'https://github.com/Raul-CV/desafio-2.git'
        //     }
        // }

        stage('Deploy') {
            steps {
                script {
                    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws-credentials-id', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                        sh """
                            aws lambda update-function-code --function-name ${LAMBDA_FUNCTION_NAME} --zip-file fileb://${ZIP_FILE_NAME}
                        """
                    }
                }
            }
        }
    }
}