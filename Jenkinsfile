pipeline {
    agent any

    tools {
        maven "Maven"
    }

    stages {

        stage('Code Analysis') {
            steps {
                echo 'Performing static code analysis'
                 sh 'mvn clean install sonar:sonar -DskipTests=true -Dsonar.sources=src/main -Dsonar.projectVersion=1.0 -Dsonar.login=admin -Dsonar.password=admin -Dsonar.java.binaries=target/classes'  
            }
        }

        stage('Build') {
            steps {
                echo 'Code Build and Unit Testing...'
                sh 'mvn clean install'
            }
        }

        stage('deploy-to-test') {
            steps {
                echo 'Deploying war in Test'
                sh 'java -cp target/jb-hello-world-maven-0.1.0.jar hello.HelloWorld'
		sh 'sleep 100'
            }
        }

        stage('FunctionalTest') {
            steps {
                echo 'Running in Functional Test'
                sh 'java -cp target/jb-hello-world-maven-0.1.0.jar hello.HelloWorld | grep DevOps'
            }
        }


 
    }

}