pipeline{
    agent {
        label 'AGENT-1'
    }
    options {
        timeout(time: 15, unit: 'MINUTES') 
        disableConcurrentBuilds()
        ansiColor('xterm')
    }
    // parameters{
    //     choice(name: 'action', choices: ['apply', 'destroy', ], description: 'apply or destriy to view the changes')
    // }
    stages{
       stage('installing dependency') {
            steps{
                sh """
                npm install 
                """
            }
        }
       stage('list') {
            steps{
                sh """
                ls -ltr
                """
            }
        }
         
    }
    post{
        always{
            echo "when pipline useing "
            deleteDir()
        }
         success{
            echo "when pipeline sucess"
        }
         failure{
            echo "when pipeline faild "
        }
    }
    
    
}
