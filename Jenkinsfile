pipeline{
    agent any {
        label 'AGENT-1'
    }
    options{
        timeout(time: 2, unit: 'SECOND')
    }
    parameters{
        choice(name: 'CHOICE', choices: ['apply', 'destroy', ], description: 'Pick something')
    }

    stages {
        stage('init') {
            steps {
                echo "trail"
            }
        }
        stage('plan') {
            steps {
                echo "trail"
            }
        }
        stage('apply') {
            steps {
                echo "trail"
            }
        }
        stage('deploy') {
            steps {
                echo "trail"
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