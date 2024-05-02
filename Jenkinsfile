pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Step 1: Build'
                echo 'Action: Utilize a build automation tool to compile and package the software.'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Step 2: Unit and Integration Testing'
                echo 'Action: Execute unit tests to verify individual code parts and perform integration tests to check interoperability of components.'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Step 3: Code Analysis'
                echo 'Action: Deploy a static code analysis tool to check code quality and adherence to standards.'
                echo 'Analysis Tool: SonarQube'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Step 4: Security Scan'
                echo 'Action: Conduct a security audit on the code to detect vulnerabilities using a specialized tool.'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Step 5: Deployment to Staging'
                echo 'Action: Deploy the software to a staging environment, such as an AWS EC2 instance.'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Step 6: Testing on Staging'
                echo 'Action: Execute integration tests in the staging setup to validate performance in a near-production scenario.'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Step 7: Production Deployment'
                echo 'Action: Roll out the software to a production server, for example, an AWS EC2 instance.'
            }
        }
    }

    post {
        always {
            emailext(
                subject: "Pipeline Status: ${currentBuild.currentResult}",
                body: """
                    Status of the Pipeline: ${currentBuild.currentResult}
                    Jenkins Page: ${env.BUILD_URL}
                    ID of Build: ${env.BUILD_NUMBER}
                """,
                attachLog: true,
                to: 'samarthmita.36@gmail.com'
            )
        }
        failure {
            when {
                expression {
                    it.name in ['Unit and Integration Tests', 'Security Scan']
                }
            }
            emailext(
                subject: "Failure in ${it.name}: ${currentBuild.currentResult}",
                body: """
                    Status of ${it.name}: ${currentBuild.currentResult}
                    Link to Jenkins: ${env.BUILD_URL}
                    Number of Build: ${env.BUILD_NUMBER}
                """,
                attachLog: true,
                to: 'samarthmita.36@gmail.com'
            )
        }
    }
}
