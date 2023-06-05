pipeline{
    
    agent any 
    
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', url: 'https://github.com/Saban39/demo-counter-app.git'
                }
            }
        }
        stage('UNIT testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn test'
                }
            }
        }
        stage('Integration testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn verify -DskipUnitTests'
                }
            }
        }
        stage('Maven build'){
            
            steps{
                
                script{
                    
                    sh 'mvn clean install'
                }
            }
        }
        stage('Static code analysis'){
            
            steps{
                
                script{
                    
                    withSonarQubeEnv(credentialsId: 'sonar-api-key') {
                        
                        sh 'mvn clean package sonar:sonar'
                    }
                   }
                    
                }
            }
            stage('Quality Gate Status'){
                
                steps{
                    
                    script{
                        
                        waitForQualityGate abortPipeline: false, credentialsId: 'sonar-api-key'
                    }
                }
            }
stage('Nexus Uploader'){
                
                steps{
                    
                    script{
                        
                       nexusArtifactUploader artifacts: [[artifactId: 'springboot', classifier: 'jar', file: 'target/Uber.jar', type: 'jar']], credentialsId: '2b8bb249-5c1b-465c-90be-7986a1f94f64', groupId: 'com.example', nexusUrl: 'nexus.example.com:9999', nexusVersion: 'nexus2', protocol: 'http', repository: 'demoapp-sg', version: '1.0.0'

                    }
                }
            }


        }
        
}
