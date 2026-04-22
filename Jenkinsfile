pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
               sh 'pipenv --python python sync'
            }
        }
        stage('Test') {
            steps {
               sh 'pipenv run pytest'
            }
        }
        stage('Package') {
	    when{
		    anyOf{ branch "master" ; branch 'release' }
	    }
            steps {
               sh 'python -m zipfile -c sbdl.zip lib'
            }
        }
	stage('Release') {
	   when{
	      branch 'release'
	   }
           steps {
              sh 'echo "Mock Deployment: Pretending to copy files to QA server..."'
           }
        }
	stage('Deploy') {
	   when{
	      branch 'master'
	   }
           steps {
               sh 'echo "Mock Deployment: Pretending to copy files to Production server..."'
           }
        }
    }
}
