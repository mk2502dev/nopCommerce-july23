pipeline{
    agent { label 'NopCommerce-node3' }
    tools{
        jdk 'JDK_17'
    }
    triggers {
        pollSCM('* * * * *')
    }
    stages{
        stage('Checkout code'){
            steps{
                git url: 'https://github.com/mk2502dev/nopCommerce-july23.git',
                    branch: 'develop'
            }
        }
        stage('Building'){
            steps{
                sh 'dotnet restore src/NopCommerce.sln'
                sh 'dotnet build -c Release src/NopCommerce.sln'
                sh 'dotnet publish -c Release src/Presentation/Nop.Web.csproj -o publish'
                sh 'mkdir publish/bin publish/logs && zip -r nopCommerce.zip publish'
                archive '**/nopCommerce.zip'
            }
        }
    }
     
}