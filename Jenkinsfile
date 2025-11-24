pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-token_shreyas',
                    url: 'https://github.com/shreyas/S_Kart2.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    def scannerHome = tool name: 'Sonar-Scanner1', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
                    withSonarQubeEnv('SonarQube-IMCC') {
                        sh """
                            ${scannerHome}/bin/sonar-scanner \
                            -Dsonar.projectKey=S_Kart2 \
                            -Dsonar.sources=. \
                            -Dsonar.host.url=http://sonarqube.imcc.com/ \
                            -Dsonar.login=sqa_119f906ec6df83a8ce2ebc11a9a772351d36bb34
                        """
                    }
                }
            }
        }

        stage('Zip Artifact') {
            steps {
                sh 'zip -r build.zip ./'
                archiveArtifacts artifacts: 'build.zip', fingerprint: true
            }
        }
    }
}
