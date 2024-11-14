pipeline
{
    agent {
        label "jenkins-agent-test"
    }

    tools {
        jdk 'Java17'
        maven 'Maven'
    }

    stages {
        stage("Cleanup Workspace") {
            steps {
                cleanWs()
            }
        }

        stage("Checkout from SCM") {
            steps {
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/networksuperman/mavenapp2'
            }
        }

        stage("Build Application") {
            steps {
                sh "mvn clean package"
            }
        }

        stage("Test Application") {
            steps {
                sh "mvn test"
            }
        }

        stage("Sonarqube Analysis") {
            steps {
                withSonarQubeEnv(credentialsID: 'jenkins-sonarqube-token') {
                    sh "mvn sonar:sonar"
                }
                
            }
        }
    }

}