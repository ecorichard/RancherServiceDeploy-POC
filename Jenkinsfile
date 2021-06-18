pipeline {
    agent { label 'kube' }
    parameters {
        string(name: 'hello')
        string(name: 'hi')
        string(name: 'hola')
    }  
    stages {
        stage('Stage-1') {
            steps {
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
