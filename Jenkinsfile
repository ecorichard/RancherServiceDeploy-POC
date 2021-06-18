pipeline {
    agent any
    parameters {
        string(name: 'hello')
        string(name: 'hi')
        string(name: 'hola')
    }  
    stages {
        stage('Stage-1') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'master',
                  credentialsId: '3e58cef0-47e7-4f65-8d45-3c5d1763e2ab',
                  url: 'https://github.com/ecorichard/RancherServiceDeploy-POC.git'
              echo "Hello World"
            }
            post {
                success {
                    echo "Successful saying hello"
                }
            }
        }
        stage('Stage-2') {
            steps {
                sh '''
                echo "Hello, time to do something"
                uname -a
                cat hello.txt | sed "s/{{ HELLO_WORLD }}/${hello}/g" | sed "s/{{ HI_WORLD }}/${hi}/g" | sed "s/{{ HOLA_WORLD }}/${hola}/g"
                '''              
            }
            post {
                success {
                    echo "Successful do something"
                }
            }
        }
        stage('Stage-3') {
            steps {
                sh "ls -la"
            }
            post {
                success {
                    echo "Successful ended"
                }
            }
        }      
    }
}
