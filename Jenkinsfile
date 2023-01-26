pipeline {
    agent any

    stages {
        stage('Test') {
            steps {
                echo 'Testing..'
		sh 'chmod 755 main.py'
		sh './main.py'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
		sh "cp main.py /usr/share/nginx/cgi-bin/main.cgi"
            }
        }
    }
}
