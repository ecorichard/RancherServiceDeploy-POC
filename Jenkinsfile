pipeline {
    agent { label 'kube' }
    parameters {
        string(name: 'hello')
        string(name: 'hi')
        string(name: 'hola')
        strubg(name: 'BUILD_VERSION')
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
                always {
                    sh '''
                    echo "BUILD_VERSION=$buildNumber" > pipelineConfig.txt
                    '''                    
                    stash includes: 'pipelineConfig.txt', name: 'pipelineConfig'
                }
            }
        }
        stage('Stage-2') {
            steps {
                unstash 'pipelineConfig'
                sh '''
                export $(grep -v '^#' pipelineConfig.txt | xargs)
                '''
                sh '''
                echo "Hello, time to do something"
                uname -a
                cat hello.txt | sed "s/{{ HELLO_WORLD }}/${hello}/g" | sed "s/{{ HI_WORLD }}/${hi}/g" | sed "s/{{ HOLA_WORLD }}/${hola}/g"
                '''            
                echo $BUILD_VERSION
            }
            post {
                success {
                    echo "Successful do something"
                }
                always {
                    sh '''
                    echo "BUILD_VERSION=$buildNumber" > pipelineConfig.txt
                    '''                    
                    stash includes: 'pipelineConfig.txt', name: 'pipelineConfig'
                }                
            }
        }
        stage('Stage-3') {
            steps {
                unstash 'pipelineConfig'   
                sh '''
                export $(grep -v '^#' pipelineConfig.txt | xargs)
                '''
                echo $BUILD_VERSION                
                sh "ls -la"
            }
            post {
                success {
                    echo "Successful ended"
                }
                always {
                    sh '''
                    echo "BUILD_VERSION=$buildNumber" > pipelineConfig.txt
                    '''                    
                    stash includes: 'pipelineConfig.txt', name: 'pipelineConfig'
                }                 
            }
        }      
    }
}
