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
                echo env.BUILD_URL
		echo 'Printing Commit Sha'
		checkout scm
		echo "Commit Sha: " + sh(returnStdout: true, script: "git log -n 1 --pretty=format:'%h'").trim()
		echo "Message: " + search_commit_msg("sand")
		
            }

        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh './foo.sh'
		echo 'Testing Complete'
            } 
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

def search_commit_msg(String msg) {
    def m = sh(returnStdout: true, script: "git log --oneline -1 -i --grep=${msg}").trim()
    if(m.contains("sand")){
    	echo "We GOOD"
    }
    if(m.contains("dans")){
    	echo "We NOT GOOD"
    }
    return m
}

def exec_downstream(){
	build job: 'Pipeline-2', parameters: [string(name: 'EXAMPLE_TEXT', value: '')]
}

