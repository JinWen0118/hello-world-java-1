pipeline {
    agent any

    environment
    {
        JAVA_HOME = "C:\\Program Files\\Java\\jdk-21"
        PATH = "${env.JAVA_HOME}\\bin;${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/JinWen0118/hello-world-java-1.git'
            }
        }
        // use gradle wrapper to build and test the project
        stage('Build') {
            steps { bat 'gradlew clean build'}
        }
        // use gradle wrapper to run the unit tests
        stage('Test') {
            steps { bat 'gradlew test'}
        }
        // use gradle wrapper to run the jar file
        stage('Deploy') {
            steps { powershell 'java -jar build/libs/hello-world-java-V1.0.jar'}           
        }    
}

post {
        always {
            // remove work directory after the build is done, regardless of the build result
            echo 'Cleaning up workspace'
            deleteDir() // Clean up the workspace after the build
        }
        success {
            echo 'Build succeeded!!!'
            // You could add notification steps here
        }
        failure {
            echo 'Build failed!'
            // You could add notification steps here
        }
    }
    
}
