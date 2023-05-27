pipeline {
    agent any
    
    tools {
        //Herramientas a utilizar
        // Necesito Maven y JDK
        //maven "nombre de herramienta  ue esta en la configuracion de globl tools configuration"
        maven "Maven"
        jdk "java11"
    }
    
    environment {
        DISABLE_AUTH = 'true'
        DB_ENGINE    = 'sqlite'
    }
    
    stages {
        stage('Hello') {
            steps {
                //echo 'Hello World'
                echo "Database engine is ${DB_ENGINE}"
                echo "DISABLE_AUTH is ${DISABLE_AUTH}"
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
                echo ""
            }
        }
        
        //stage('Descargar código de git'){
        stage('Git Polling')
        {    
           steps 
            {
            
            //git branch: 'master', url:'https://github.com/PabloRiverosA/time-tracker.git'
            git branch: 'master', credentialsId: 'JenkisGit-PabloRiverosA', url: 'git@github.com:PabloRiverosA/time-tracker.git'
            
            }
            
        }
        
        stage ('BUILD CON MAVEN'){
        steps {
            bat "mvn clean package -DsKipTests" //Windows
            
                }
        post{
            success{
                echo 'Archivar Artefactos'
                archiveArtifacts "/core/target/*.jar"
                archiveArtifacts "/web/target/*.war"

            }
                    }
        }
        
        stage ('Test Maven'){
            steps {
                bat "mvn test"
                
            }
        }
        
    }
}
