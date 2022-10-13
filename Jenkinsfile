pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
                git branch: 'main', url: 'git@github.com:sivaram2662/sample-code.git'
               
            }
        }
        stage('ci') {
            steps {
                sh '''
                zip -r static-app-$BUILD_NUMBER.zip *
                aws s3 cp static-app-$BUILD_NUMBER.zip s3://ram-bucker/
               '''
            }
        }
        stage('cd') {
            steps {
                sh '''
                rm -rf *
                aws s3 cp s3://ram-bucker/static-app-$BUILD_NUMBER.zip .
                unzip static-app-$BUILD_NUMBER.zip
                ls 
                scp index.html root@172.31.46.218:/var/www/html/
                
               ''' 
            }  
        }   
    }
}