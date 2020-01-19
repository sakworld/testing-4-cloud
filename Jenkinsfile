pipeline {
    agent { label 'master'}

    parameters{
        string(name:'AWS_ACCESS_KEY', defaultValue: '', description: 'AWS_ACCESS_KEY')
        string(name:'AWS_SECRET_ACCESS_KEY', defaultValue: '', description: 'AWS_SECRET_ACCESS_KEY')
    }
    stages {
        stage('Terraform Install'){
            steps{
                  sh(
                      '''
                      sh 'scripts/terraform-install.sh'
        
                      '''  
                  )
            }

        }
        stage('Terraform init'){
            steps{
                  sh(
                      '''
                      sh 'scripts/terraform-init.sh'
                      '''  
                  )
            }

        }
        stage('Terraform Plan'){
            steps{
                  sh(
                      '''
                      sh 'scripts/terraform-plan.sh'
                      '''  
                  )
            }
        }
        stage('Terraform apply'){
            steps{
                  sh(
                      '''
                      sh 'scripts/terraform-apply.sh'
                      '''  
                  )
            }
        }
        stage('Terraform out'){
            steps{
                  sh(
                      '''
                      sh 'scripts/terraform-out.sh'
                      '''  
                  )
            }
        }
        stage('Inspec  install'){
            steps{
                  sh(
                      '''
                      sh 'scripts/inspec-install.sh'
                      '''  
                  )
            }
        }
        stage('Run infra Tests') {
        parallel {
            stage('Inspec') {
              steps {
                script {
                    def exists = fileExists 'aws-terraform/test/verify'
                    if (exists) {
                        sh 'scripts/inspec.sh'
                        } 
                        else 
                        { 
                            echo "test/veriry directory not found" 
                        }
                    }
                }
            }
              stage('Behave') {
              steps {
                script {
                    def exists = fileExists 'aws-terraform/test/behave'
                    if (exists) {
                        echo "Behave Tests - Yet to be defined"
                        } 
                        else 
                        { 
                            echo "behave/test/veriry directory not found" 
                        }
                    }
                }
            }
          }
        }
        stage('Terra destroy'){
            steps{
                  sh(
                      '''
                      sh 'scripts/terraform-destroy.sh'
                      '''  
                  )
            }
        }
    }
}
