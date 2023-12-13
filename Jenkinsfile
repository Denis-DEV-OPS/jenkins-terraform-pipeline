pipeline {
    agent any
    stages {
        stage('Preparing') {
            steps {
                sh 'echo Preparing'
            }
        }
        stage('Git Pulling') {
            steps {
                git branch: 'main', url: 'https://github.com/Denis-DEV-OPS/jenkins-terraform-pipeline.git'
                sh 'ls'
            }
        }
        stage('Init') {
            steps {
                echo "Enter File Name ${params.File_Name}"
                echo "Pipeline Name ${params.Pipeline}"
                withAWS(credentials: '7b5c6ae5-aef1-4049-8c6f-390b3dd64935', region: 'us-east-1') {
                }
            }
        }
        
        stage('Action') {
            steps {
                echo "${params.Terraform_Action}"
                withAWS(credentials: '7b5c6ae5-aef1-4049-8c6f-390b3dd64935', region: 'us-east-1') {
                sh 'terraform get -update' 
                    script {    
                        if (params.Terraform_Action == 'plan') {
                            sh 'terraform -chdir=Non-Modularized/${File_Name}/ plan --lock=false'
                        }   else if (params.Terraform_Action == 'apply') {
                            sh 'terraform -chdir=Non-Modularized/${File_Name}/ apply --lock=false -auto-approve'
                        }   else if (params.Terraform_Action == 'destroy') {
                            sh 'terraform -chdir=Non-Modularized/${File_Name}/ destroy --lock=false -auto-approve'
                        } else {
                            error "Invalid value for Terraform_Action: ${params.Terraform_Action}"
                        }
                    }
                }
                
            }
        }
    }
}
