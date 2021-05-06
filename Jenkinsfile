pipeline {
    agent any 
    stages{
        stage('Build') { 
            steps {
                echo 'Start building'
                sh 'git pull origin master'
                sh 'npm install'
                sh 'npm build'
            }
             post 
        failure {
            emailext attachLog: true,
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                recipientProviders: [developers(), requestor()],
                to: 'karolc3dro@gmail.com',
                subject: "Build failed in Jenkins ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
        }
        success {
            emailext attachLog: true,
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                recipientProviders: [developers(), requestor()],
                to: 'karolc3dro@gmail.com',
                subject: "Successful build in Jenkins ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
        }
    }
            
        } 
        stage('Test') { 
            steps {
                echo 'Start testing'
                sh 'npm test'
            }
             post {
        failure {
            emailext attachLog: true,
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                recipientProviders: [developers(), requestor()],
                to: 'karolc3dro@gmail.com',
                subject: "Test failed in Jenkins ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
        }
        success {
            emailext attachLog: true,
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                recipientProviders: [developers(), requestor()],
                to: 'karolc3dro@gmail.com',
                subject: "Successful test in Jenkins ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
        }
    }
        } 
    }

}
