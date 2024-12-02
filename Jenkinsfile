pipeline {
    agent any
    
    environment {
        // Set environment variables for GitHub and Tomcat
        GIT_REPO = 'https://github.com/SagarTripurana/maven-new-springboot.git' // Change to your repo URL
        TOMCAT_HOME = '/opt/tomcat' // Change to your Tomcat installation path
        TOMCAT_USER = 'sagar' // Tomcat login username
        TOMCAT_PASS = 'password' // Tomcat login password
    }

    stages {
        stage('Checkout Code') {
            steps {
                script {
                    // Checkout the latest code from GitHub
                    git branch: 'main', url: "$GIT_REPO"
                }
            }
        }
        
        stage('Build') {
            steps {
                script {
                    // Run Maven build (use Gradle or other build tool if needed)
                    sh 'mvn clean install -DskipTests=true' // Adjust if you're using Gradle
                }
            }
        }
        
        stage('Test') {
            steps {
                script {
                    // Run Maven tests
                    sh 'mvn test'
                }
            }
        }

        stage('Package WAR') {
            steps {
                script {
                    // Package the application into a WAR file
                    sh 'mvn package'
                }
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                script {
                    // Deploy WAR file to Tomcat using Tomcat Manager (ensure tomcat manager is installed and accessible)
                    def warFile = 'target/Springdemo-0.0.1-SNAPSHOT.war' // Update to your generated WAR file path
                    def tomcatUrl = "http://34.228.65.128:8080/manager/text"
                    
                    sh """
                    curl -u $TOMCAT_USER:$TOMCAT_PASS \
                        -T $WAR_FILE \
                        "$TOMCAT_URL/deploy?path=/Springdemo-0.0.1-SNAPSHOT&update=true"
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs for errors.'
        }
    }
}
