pipeline {
    agent any
        triggers {
            //pollSCM('') //Empty quotes tells it to build on a push  
            githubPush()
        }
        stages {
            stage('Build') {
                steps {
                    echo 'This is the Build Stage'
                }
            }
            stage('Test') {
                steps {
                    echo 'This is the Testing Stage'
                }
            }
            stage('Deploy') {
                steps {
                    sshagent(credentials : ['dbd5d967-04bd-11eb-b4c0-fa163e0fc7ce']) {                    
                        echo 'This is the Deploy Stage'
                        sh 'ssh -v bp000383@ela1.cscs.ch "mkdir -p ./bin/new_code" '
                        sh 'scp * bp000383@ela1.cscs.ch:~/bin/new_code'
                        sh 'ssh -v bp000383@ela1.cscs.ch "./bin/execute_daint.sh" '
                    }
                }
            }
        }
    }
