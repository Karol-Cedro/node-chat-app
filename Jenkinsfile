pipeline {
    agent any
    stages{
        stage('Build') {
            steps {
                echo 'Start building'
                sh 'git pull origin master'
                sh 'npm install'
            }

        post{
            failure {
                emailext attachLog: true,
                    body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                 recipientProviders: [developers(), requestor()],
                    to: 'karolc3dro@gmail.com',
                    subject: "Build failed : Job ${env.JOB_NAME}"
            }
            success {
            emailext attachLog: true,
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                recipientProviders: [developers(), requestor()],
                to: 'karolc3dro@gmail.com',
                subject: "Build successful : Job ${env.JOB_NAME}"
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
                subject: "Test failed : Job ${env.JOB_NAME}"
        }
        success {
            emailext attachLog: true,
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                recipientProviders: [developers(), requestor()],
                to: 'karolc3dro@gmail.com',
                subject: "Test successful : Job ${env.JOB_NAME}"
        }
        }
        }
        stage('Deploy') {
            steps {
                echo 'Start deploying'
                sh 'docker build -t deploy -f docker-deploy .'
                
            }
        post {
        failure {
            emailext attachLog: true,
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                recipientProviders: [developers(), requestor()],
                to: 'karolc3dro@gmail.com',
                subject: "Deploy failed : Job ${env.JOB_NAME}"
        }
        success {
            emailext attachLog: true,
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                recipientProviders: [developers(), requestor()],
                to: 'karolc3dro@gmail.com',
                subject: "Deploy successful : Job ${env.JOB_NAME}"
        }
        }
        }
    }

}
