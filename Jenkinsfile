pipeline{
    agent {
        label 'AGENT-1'
    }
    options{
        timeout(time: 2, unit: 'MINUTES')
        ansiColor('xterm')
        disableConcurrentBuilds()
    }
    // parameters{
    //     choice(name: 'CHOICE', choices: ['apply', 'destroy', ], description: 'Pick something')
    // }

    stages {  
        stage('init list out the file ') {
            steps {
                sh"""
                ls -ltr
                """
            }
        }
        stage('instll dependencies ') { // This stage should be inside the 'stages' block
        steps {
            sh"""
            npm install 
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
