pipeline{
    agent {
        label 'AGENT-1'
    }
    options{
        timeout(time: 2, unit: 'MINUTES')
        ansiColor('xterm')
        disableConcurrentBuilds()
    }
    parameters{
        choice(name: 'CHOICE', choices: ['apply', 'destroy', ], description: 'Pick something')
    }

    stages {
        stage('init') {
            steps {
                sh"""
                ls -ltr
                """
            }
        }
        
    }

    post {
        always{
           echo " ill alls run"
           deleteDir()
        }
        success {
            echo "this will run when code sucess"
        }

        failure {
            echo "this will run when code filed"
        }
    }
}