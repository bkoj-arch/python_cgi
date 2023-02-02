pipeline {
    agent agent

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
		sh "sftp jenkins@1.2.3.40:~/cgi-bin/ <<EOF\
			put main.cgi\
		EOF"
            }
        }
    }
}
