// # Online Python compiler (interpreter) to run Python online.
// # Write Python 3 code in this online editor and run it.

@Library('shared-library') _
pipeline {
    agent any 
    
    // environment {
    //     WAR_PATH= ""
    // }
    
    stages{
        stage("Git Checkout") {
            steps {
                sh "echo Git checkout"
                
                git branch: "main", url: "https://github.com/rajendraprasad10/spring-boot-mongo-docker-devsecops.git"
            }
        }
        
        stage("Code Compile") {
            steps {
                sh "echo Code Compile"
                sh "mvn compile"
            }
        }
        
        stage("Unit Testing") {
            steps {
                sh "echo unit testing"
                sh "mvn test"
            }
        }
        
        stage("SAST") {
            steps {
                sh "echo SAST"
                sh "mvn sonar:sonar"
            }
        }
        
        stage("Synk") {
            steps {
                sh "echo Synk"
                
            }
        }
        
        stage("Dependency Check") {
            steps {
                sh "echo dependency check"
                
            }
        }
        
        stage("Build") {
            steps {
                sh "echo echo Build"
                sh "mvn package"
            }
        }
        
        stage("Docker Image Build") {
            steps {
                sh "echo echo Image build"
                sh "docker build -t orm-backend:1.0.1 ."
            }
        }
        
        stage("Docker Image Scanning"){
            steps {
                sh "echo docker image scanning"
                sh """trivy image orm-backend:1.0.1 \
            --severity HIGH,CRITICAL \
            --format table \
            --output trivy-report.table \
            --exit-code 0 """
            }
        }
        
        stage("Deployemnt Approval"){
            steps {
                sh "echo deployment approval"
                
            }
        }
        
        stage("Push to Registry"){
            steps {
                sh "echo Push to Registry"
            }
        }
        
        stage("deploy"){
            steps {
                sh "echo deploy..."
                // sh "mvn deploy"
            }
        }
        
        
    }

    
    post {
        
        always {
            archiveArtifacts artifacts: 'trivy-report.table'
        }

        success {
            sh "echo build sucess..."
            sh "echo slack notification setup!"
        }
        
        failure {
            sh "echo build failed..."
            sh "echo slack notification setup!"
        }
        
    
}

}






