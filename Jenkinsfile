pipeline {
    agent any

    tools {
        maven "maven-3.6.2"
    }

    stages {
        stage('Build') {
            steps { 
                git branch: 'main', url: 'https://github.com/slesha-abb/payment-app.git'
                sh "mvn -Dmaven.test.failure.ignore=true clean install sonar:sonar -Dsonar.host.url='http://172.31.27.16:9000/'"
            }
            post {
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
          }
        stage('deploy') {
                steps {
                    sh 'echo deployment process started'
                }
                post {
                    success {
                        sh 'echo deployment process completed'
                    }
                }
            }
    }
}
