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
        stage('read the version'){
            steps{
                // The following lines should be inside a script block
                def packageJson = readJSON file: 'package.json'
                def appVersion= packageJson.version
                echo "application version is: $appVersion"
            }
        }
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
                // The following line won't work as appVersion is not accessible in this shell script
                echo "application version is: $appVersion"
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
} // Missing closing brace for the pipeline block
