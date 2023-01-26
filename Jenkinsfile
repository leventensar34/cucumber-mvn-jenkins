pipeline {
    agent any
    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "3.0"
    }    
    stages {
        stage('Build') {
            steps {
                sh 'mvn -f Cucumber/pom.xml -B -DskipTests clean package'
            }
            post {
                success {
                    echo "Now Archiving the Artifacts....."
                    archiveArtifacts artifacts: '**/*.jar'
                }
            }
        }
        stage('Test') {
            steps {
                sh 'mvn -f Cucumber/pom.xml test'
                sh 'mvn clean verify'
            }
            post {
                always {
                    junit 'Cucumber/target/surefire-reports/*.xml'
                    html 'target/cucumber-report.html'
                }
            }
        }
    }
}
