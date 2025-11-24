pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-token',
                    url: 'https://github.com/shreyas/S_Kart2.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube-IMCC') {
                    sh '''
                        sonar-scanner \
                        -Dsonar.projectKey=S_Kart2 \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=http://sonarqube.imcc.com/ \
                        -Dsonar.login=sqa_119f906ec6df83a8ce2ebc11a9a772351d36bb34
                    '''
                }
            }
        }

        stage('Build') {
            steps {
                echo 'No build needed for HTML/CSS/JS project'
            }
        }

        stage('Archive Artifact') {
            steps {
                sh 'zip -r build.zip ./'
                archiveArtifacts artifacts: 'build.zip', fingerprint: true
            }
        }
    }
}
