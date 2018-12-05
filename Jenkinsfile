node{
    agent any
       parameters {
       string(name: 'EXAMPLE_TEXT', defaultValue: '', description: 'Example Text for Parameterization')
       string(name: 'SCRIPT_ARGS', defaultValue: '', description: 'Script Args')
   }

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
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
	stage ('Triggering Downstream Jobs') {
            if ("$env.TRIGGER_DOWNSTREAM_JOB".toBoolean()) {
                echo "Triggering ddoc-poker-test job..."
                exec_downstream()
            } else {
                echo "Not triggering downstream jobs."
            }
        }
}

def exec_downstream(){
	build job:
        'Pipeline-2',
        parameters: [
            [$class: 'StringParameterValue', name: 'SCRIPT_ARGS', value: "${env.SCRIPT_ARGS}"],
        ],
        wait: false
}
