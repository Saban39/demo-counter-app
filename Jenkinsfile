pipeline{
    
    agent any 
    tools {
        maven 'maven'
    }
    stages {
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', url: 'https://github.com/Saban39/demo-counter-app.git'
                }
            }
        }
       
stage('Nexus Uploader'){
                
                steps{
                    
                    //groovy.lang.MissingPropertyException: No such property: readMavenPom for class: groovy.lang.Binding

                    script{
                        
                       def readPomVersion  = readMavenPom file: 'pom.xml'
                       def nexusRepo  = readPomVersion.version.endsWith("SNAPSHOT") ? "demoapp-snapshot" : "demoapp-sg"
                       nexusArtifactUploader artifacts: [[artifactId: 'springboot', classifier: '', file: 'target/Uber.jar', type: 'jar']], credentialsId: '2b8bb249-5c1b-465c-90be-7986a1f94f64', groupId: 'com.example', nexusUrl: 'nexus.example.com:9999', nexusVersion: 'nexus3', protocol: 'http', repository: nexusRepo, version: "${readPomVersion.version}"

                    }
                }
            }


        }
        
}
