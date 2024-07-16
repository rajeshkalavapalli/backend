pipeline{
    agent {
        label 'AGENT-1'
    }
    options {
        timeout(time: 15, unit: 'MINUTES') 
        disableConcurrentBuilds()
        ansiColor('xterm')
    }
    environment{
        def appVersion = ''
        def nexusUrl='54.235.229.243:8081/repository/backend'
    }
    // parameters{
    //     choice(name: 'action', choices: ['apply', 'destroy', ], description: 'apply or destriy to view the changes')
    // }
    stages{
        stage('read the version'){
            steps{
                script{
                    def packageJson = readJSON file: 'package.json'
                    appVersion = packageJson.version
                    echo "application version: $appVersion"
                }
                
            }
        }
       stage('Install Dependencies') {
            steps {
               sh """
                npm install
                ls -ltr
                echo "application version: $appVersion"
               """
            }
        }  
        stage('build') {
            steps {
               sh """
                zip backend-${appVersion}.zip * -x jenkinsfile -x backend-${appVersion}.zip
                ls -ltr
               """
            }
        }
        stage('Nexus Artifact Uploading') {
            steps {
                script {
                    nexusArtifactUploader(
                        nexusVersion: 'nexus3',
                        protocol: 'http',
                        nexusUrl: "${nexusUrl}",
                        groupId: 'com.expense',
                        version: "${appVersion}",
                        repository: 'backend',
                        credentialsId: 'nexus-pass',
                        artifacts: [
                            [
                                artifactId: "backend",
                                classifier: '',
                                file: "backend-${appVersion}.zip",
                                type: 'zip'
                            ]
                        ]
                    )
                }
            }
        }
        stage('Deploy'){
            when{
                expression{
                    params.deploy
                }
            }
            steps{
                script{
                    def params = [
                        string(name: 'appVersion', value: "${appVersion}")
                    ]
                    build job: 'backend-deploy', parameters: params, wait: false
                }
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
