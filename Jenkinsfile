pipeline {
    agent any
       parameters {
       string(name: 'EXAMPLE_TEXT', defaultValue: '', description: 'Example Text for Parameterization')
   }

   
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                echo "${params.EXAMPLE_TEXT}"
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh './foo.sh'
            }
            env.BUILD_URL
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
	}
	stage('Trigger Downstream'){
	    steps{
	   	echo 'Trigger Downstream job....'
		exec_downstream()
	    }	
	}
    }
}

def exec_downstream(){
	build job: 'Pipeline-2', parameters: [string(name: 'EXAMPLE_TEXT', value: '')]
}

