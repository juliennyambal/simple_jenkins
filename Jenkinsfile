pipeline {
    agent { 
        node {
            label 'docker-agent-python'
            }
      }
    triggers {
        pollSCM '* * * * *'
    }
    stages {
	    stage('Pull Repo') {
            steps {
                echo "Pulling repo.."
                sh '''
                FOLDER="simple_jenkins"
                URL="https://github.com/juliennyambal/simple_jenkins.git"
                if [ ! -d "$FOLDER" ] ; then
                    git clone "$URL"
                fi
				cd myapp
                '''
            }
        }
	    stage('Lib Intallation') {
            steps {
                echo "Virtual Environment.."
                sh '''
				cd myapp
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
                cd myapp
                . ./jenkins_venv/bin/activate
                python3 -m pytest -v
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