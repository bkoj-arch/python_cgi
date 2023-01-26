pipeline {
    agent any

    stages {
        stage('Test') {
            steps {
                echo 'Testing..'
		sh 'chmod 755 main.py'
		sh './main.py'
sh 'pylint --disable=W1202 --output-format=parseable --reports=no module > pylint.log || echo "pylint exited with $?")'
sh 'cat render/pylint.log'

step([
        $class                     : 'WarningsPublisher',
        parserConfigurations       : [[
                                              parserName: 'PYLint',
                                              pattern   : 'pylint.log'
                                      ]],
        unstableTotalAll           : '0',
        usePreviousBuildAsReference: true
])
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
