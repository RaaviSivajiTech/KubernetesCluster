
pipeline {    
    environment {
        AWS_ACCESS_KEY_ID     = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
        AZURE_SUBSCRIPTION_ID = credentials('AZURE_SUBSCRIPTION_ID')
        AZURE_CLIENT_ID = credentials('AZURE_CLIENT_ID')
        AZURE_CLIENT_SECRET = credentials('AZURE_CLIENT_SECRET')
        AZURE_TENANT_ID = credentials('AZURE_TENANT_ID')
    }
   agent  any
    stages {
        stage('checkout') {
            steps {
                 script{
                        dir("terraform")
                        {
                            git "https://github.com/RaaviSivajiTech/PetclinicApp.git"
                        }
                    }
                }
            }

        stage('Plan') {
            steps {
                 withCredentials([azureServicePrincipal('ARM_CRED')]) {
                    
                    sh 'echo "Azure Cluster Infrastructure provisioning started"'
                    
                    sh "pwd;cd Azure/Scripts/; pwd; ls;"

                    sh "sudo chmod 777 azureinfra.sh"

                    sh "./azureinfra.sh;"

                    sh 'echo "Azure Cluster Infrastructure provisioning started"'
                }
            }
        }      
    }
  }
