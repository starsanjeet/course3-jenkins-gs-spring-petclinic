pipeline {
    agent any
    stages {
        stage("checkout") {
            steps {
                git branch:'main', url: 'https://github.com/starsanjeet/course3-jenkins-gs-spring-petclinic'
            }
        }
        stage("build") {
            steps {
                bat "mvnw.cmd package"
            }
        }
        stage("capture") {
            steps{
                archiveArtifacts '**/target/*.jar'
                junit '**/target/surefire-reports/TEST*.xml'
                jacoco()
            }
        }
    }
    post {
        always {
            mail body: "${env.BUILD_URL}\n${currentBuild.absoluteUrl}",subject: "${currentBuild.currentResult}: Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]", to: 'starsanjeet.shop@gmail.com'
        }
    }
}