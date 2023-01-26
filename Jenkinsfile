pipeline {
    agent any

    stages {
        stage('Test') {
            steps {
                echo 'Testing..'
		chmod 755 main.py
		./main.py
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
		sh 'cp main.py /usr/share/nginx/cgi-bin/main.cgi'
            }
        }
    }
}
