pipeline {
    agent any
    triggers {
        pollSCM '* * * * *'
    }
    stages {
	    stage('Pull Repo') {
            steps {
                echo "Pulling repo.."
                sh '''
                git clone https://github.com/juliennyambal/simple_jenkins.git
				cd add
                '''
            }
        }
	    stage('Lib Intallation') {
            steps {
                echo "Virtual Environment.."
                sh '''
				cd add
                python3 -m venv jenkins_venv
				. ./jenkins_venv/bin/activate
                pip install -r requirements.txt
                '''
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."

                sh '''
                cd add
                . ./jenkins_venv/bin/activate
                python3 -m pytest
                '''
            }
        }
        stage('Deliver') {
            steps {
                echo 'Deliver....'
                sh '''
                echo "doing delivery stuff.."
                '''
            }
        }
    }
}