pipeline {
    agent any

    environment {
        // GitHub repository details
        GIT_REPO = 'https://github.com/SagarTripurana/maven-new-springboot.git' // Replace with your repo
        GIT_BRANCH = 'main'  // Replace with the branch you want to use

        // Tomcat Manager details
        TOMCAT_URL = 'http://34.228.65.128:8080/manager/text'
        TOMCAT_USER = 'sagar'  // Replace with your Tomcat manager username
        TOMCAT_PASS = 'password'  // Replace with your Tomcat manager password

        // Path to your WAR file (change if necessary)
        WAR_FILE = 'target/Springdemo-0.0.1-SNAPSHOT.war'

        // Optional: GitHub credentials, use Jenkins credentials manager for more secure handling
        
    }
#####
    stages {
        stage('Checkout Code') {
            steps {
                script {
                    // Checkout the code from GitHub repository
                    git branch: GIT_BRANCH, url: GIT_REPO
                }
            }
        }

        stage('Build and Test') {
            steps {
                script {
                    // Run Maven to build and test the project
                    sh 'mvn clean install'  // Adjust to your build tool (e.g., Maven or Gradle)
                }
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                script {
                    // Deploy the WAR file to Tomcat using curl
                    sh """
                    curl -u $TOMCAT_USER:$TOMCAT_PASS \
                        -T $WAR_FILE \
                        "$TOMCAT_URL/deploy?path=/Springdemo-0.0.1-SNAPSHOT&update=true"
                    """
                }
            }
        }
    }
######
    #####
    post {
        success {
            echo 'Deployment to Tomcat was successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
