//updating here to test auto trigger
pipeline {
    agent any

    environment {
        DIRECTORY_PATH = 'src/main/code'
        TESTING_ENVIRONMENT = 'staging'
        PRODUCTION_ENVIRONMENT = 'production-server'
    }

    triggers {
        pollSCM('* * * * *')
    }

    stages {

        stage('Build') {
            steps {
                echo "Stage 1 - Build"
                echo "Tool: Maven"
                echo "Action: Compiling source code from ${DIRECTORY_PATH} and packaging into a deployable artifact using Maven (mvn clean package)."
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo "Stage 2 - Unit and Integration Tests"
                echo "Tools: JUnit (unit tests), Selenium (integration tests)"
                echo "Action: Running unit tests with JUnit to verify individual components, then running integration tests with Selenium to ensure all components work together correctly."
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Stage 3 - Code Analysis"
                echo "Tool: SonarQube"
                echo "Action: Analysing source code with SonarQube to detect code smells, bugs, and ensure the codebase meets industry quality standards."
            }
        }

        stage('Security Scan') {
            steps {
                echo "Stage 4 - Security Scan"
                echo "Tool: OWASP Dependency-Check"
                echo "Action: Scanning project dependencies with OWASP Dependency-Check to identify known CVEs and security vulnerabilities in third-party libraries."
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Stage 5 - Deploy to Staging"
                echo "Tool: AWS CLI / Ansible"
                echo "Action: Deploying the application to the staging environment (${TESTING_ENVIRONMENT}) on an AWS EC2 instance."
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Stage 6 - Integration Tests on Staging"
                echo "Tool: Postman / Newman"
                echo "Action: Running API integration tests on the staging environment using Postman/Newman to ensure the application behaves correctly in a production-like setup."
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Stage 7 - Deploy to Production"
                echo "Tool: AWS CLI / Ansible"
                echo "Action: Deploying the verified application to the production server (${PRODUCTION_ENVIRONMENT}) on AWS EC2 after all tests and approvals have passed."
            }
        }

    }

    post {
        success {
            echo "Pipeline completed successfully. Application deployed to production."
        }
        failure {
            echo "Pipeline failed. Check the logs for errors."
        }
    }
}