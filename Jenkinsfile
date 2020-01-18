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
        stage("Terraform Tests"){
             parallel {
                 stage('inspec'){
                 steps {
                   "InSpec Verifcation" {
                   def exists = fileExists 'test/verify'
                   if (exists) {
                   sh "echo terraform output here"
                   sh "echo inspec exec here"
          } else {
            echo "No InSpec Verification Tests to Run."
          }
        }
     }
    }            
                stage('behave'){
                "Behave"{
                 def exists = fileExists 'test/features'
                 if (exists) {
                 sh "echo behave exec here"
                 } else {
            echo "No Behave Functional Tests to Run."
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