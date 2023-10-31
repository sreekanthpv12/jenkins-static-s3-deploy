pipeline {
    agent any
    environment {
        build_number = "${env.BUILD_ID}"
        AWS_ACCOUNT_ID = "723466211632"
        AWS_DEFAULT_REGION = "us-east-1"
    }
      tools {
        maven 'maven'
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    git branch: 'main', url: 'https://github.com/sreekanthpv12/jenkins-static-s3-deploy.git'
                }
            }
        }

         stage('Deploy to S3') {
            steps {
                script {
             
               
                 withCredentials([aws(credentialsId: 's3-credential', accessKeyVariable: 'AWS_ACCESS_KEY_ID', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                        
                        
                    sh "aws s3 cp public/index.html s3://my-static-bucket-jenkins320132/"
                    sh "aws s3 cp public/error.html s3://my-static-bucket-jenkins320132/"
                 }
                 
            
            }
          }
        }

        stage('Set Bucket Policy') {
            steps {
                script {
             
               
                 withCredentials([aws(credentialsId: 's3-credential', accessKeyVariable: 'AWS_ACCESS_KEY_ID', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                        
                        
                sh "aws s3api put-bucket-policy --bucket my-static-bucket-jenkins320132 --policy file://your-policy.json"
            }
        }
            }
        }
    }
}
