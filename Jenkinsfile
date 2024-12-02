pipeline {
    agent any
    
    environment {
        // Set environment variables for GitHub and Tomcat
        GIT_REPO = 'https://github.com/your-repo/your-project.git' // Change to your repo URL
        TOMCAT_HOME = '/path/to/tomcat' // Change to your Tomcat installation path
        TOMCAT_USERNAME = 'yourTomcatUsername' // Tomcat login username
        TOMCAT_PASSWORD = 'yourTomcatPassword' // Tomcat login password
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
                    def warFile = 'target/your-app.war' // Update to your generated WAR file path
                    def tomcatUrl = "http://localhost:8080/manager/text/deploy?path=/your-app&war=file://$PWD/$warFile"
                    
                    sh """
                    curl -u $TOMCAT_USERNAME:$TOMCAT_PASSWORD "$tomcatUrl"
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
