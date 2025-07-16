pipeline {
    agent any

    stages{
        stage("Cloning from GitHub..."){
            steps{
                echo 'Cloning from GitHub...'
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-token', url: 'https://github.com/Snehallaldas/MLOPS-PROJECT2.git']])
            }
        }
    }
}