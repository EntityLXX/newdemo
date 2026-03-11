pipeline {
    agent any
    tools {
        maven 'M3' // Ensure this matches your Jenkins Tool name
    }
    stages {
        stage('Cleanup Old Deployments') {
            steps {
                // Force delete old folders/files to prevent "Zip END header" errors
                bat 'if exist "C:\\tomcat10\\webapps\\ROOT.war" del /f /q "C:\\tomcat10\\webapps\\ROOT.war"'
                bat 'if exist "C:\\tomcat10\\webapps\\ROOT" rd /s /q "C:\\tomcat10\\webapps\\ROOT"'
            }
        }
        stage('Build') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }
        stage('Deploy to C:\\tomcat10') {
            steps {
                bat 'copy target\\*.war "C:\\tomcat10\\webapps\\ROOT.war" /Y'
            }
        }
    }
}