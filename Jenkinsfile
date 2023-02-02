pipeline {
    agent any

    stages {
        stage('Test') {
            steps {
                echo 'Testing..'
		sh 'chmod 755 main.py'
	sh 'python3 -m pylint --output-format=parseable  main.py --msg-template="{path}:{line}: [{msg_id}({symbol}), {obj}] {msg}" | tee pylint.log || echo "pylint exited with $?"'
echo "linting Success, Generating Report"
recordIssues enabledForFailure: true, aggregatingResults: true, tool: pyLint(pattern: 'pylint.log')
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
