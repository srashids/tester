pipeline {
    agent any
    node {
    checkout scm 
    /* .. snip .. */
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            when {
              expression {
                currentBuild.result == null || currentBuild.result == 'SUCCESS' 
              }
            steps {
                echo 'Deploying....'
                echo "Roses are red, violets are blue...."
            }
        }
    }
}