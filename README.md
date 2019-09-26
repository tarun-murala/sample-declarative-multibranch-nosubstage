# sample-declarative-multibranch-nosubstage
Sample Declarative Multibranch Pipeline


```
pipeline {
    agent {
        tools { 
            maven 'Maven' 
        }
    }
    stages {
        stage('Checkout') {
            steps {
                snDevOpsStep()
                checkout scm
            }
        }
        stage('Build') {
            steps {
                snDevOpsStep()
                sh 'mvn clean install'
            }
        }
        stage('Test') {
            steps {
                snDevOpsStep()
                sh "mvn test"
            }
        }
        stage('Deliver for development') {
            when {
                branch 'dev' 
            }
            steps {
                snDevOpsStep()
                // sh "mvn -B deploy"
                // sh "mvn -B release:prepare"
                // sh "mvn -B release:perform"
                // deploy using kubernetes - kubectl
                echo "Deploy"
            }
        }
        stage('Deploy for production') {
            when {
                branch 'master'  
            }
            steps {
                snDevOpsStep()
                // sh "mvn -B deploy"
                // sh "mvn -B release:prepare"
                // sh "mvn -B release:perform"
                // deploy using kubernetes - kubectl
                echo "Deploy"
            }
        }
    }
}
```
