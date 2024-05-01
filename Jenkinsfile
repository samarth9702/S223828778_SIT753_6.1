pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Stage 1: Build'
                echo 'Task: Build the code using a build automation tool to compile and package your code.'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Unit and Integration Tests'
                echo 'Task: Run unit tests to ensure the code functions as expected, and run integration tests to ensure the different components of the application work together as expected.'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Code Analysis'
                echo 'Task: Integrate a code analysis tool to analyze the code and ensure it meets industry standards.'
                echo 'Tool: SonarQube'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Stage 4: Security Scan'
                echo 'Task: Perform a security scan on the code using a tool to identify any vulnerabilities.'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploy to Staging'
                echo 'Task: Deploy the application to a staging server (e.g., AWS EC2 instance).'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Integration Tests on Staging'
                echo 'Task: Run integration tests on the staging environment to ensure the application functions as expected in a production-like environment.'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploy to Production'
                echo 'Task: Deploy the application to a production server (e.g.,AWS EC2 instance).'
            }
        }
    }

    post {
        always {
            emailext (
                subject: "Pipeline Status: ${currentBuild.currentResult}",
                body: """
                    Pipeline Status: ${currentBuild.currentResult}
                    Jenkins URL: ${env.BUILD_URL}
                    Build Number: ${env.BUILD_NUMBER}
                """,
                attachLog: true,
                to: 'samarthmita.36@gmail.com'
            )
        }
        failure {
            when {
                expression {
                    it.name == 'Unit and Integration Tests' || it.name == 'Security Scan'
                }
            }
            emailext (
                subject: "${it.name} Stage Failed: ${currentBuild.currentResult}",
                body: """
                    ${it.name} Stage Status: ${currentBuild.currentResult}
                    Jenkins URL: ${env.BUILD_URL}
                    Build Number: ${env.BUILD_NUMBER}
                """,
                attachLog: true,
                to: 'samarthmita.36@gmail.com'
            )
        }
    }
}
