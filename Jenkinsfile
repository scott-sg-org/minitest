pipeline {
    agent any

    environment {
        SEMGREP_APP_TOKEN = credentials('SEMGREP_APP_TOKEN')
    }


    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "Maven-3"
    }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/scott-sg-org/minitest.git'

                // Run Maven on a Unix agent.
                sh "mvn -DskipTests=true clean package"
            }
        }
        stage('Semgrep code analysis') {
            agent {
                docker { image 'semgrep/semgrep:latest' }
            }
            steps {
                sh 'semgrep ci'
            }
        }
    }
}
