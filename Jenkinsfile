pipeline {
    agent any

    environment{
        VENV_DIR = 'venv'
    }

    stages{
        stage("Cloning from GitHub..."){
            steps{
                script{
                    echo 'Cloning from GitHub...'
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-token', url: 'https://github.com/Snehallaldas/MLOPS-PROJECT2.git']])
                }
            }
        }

        stage("Making the virtual environment..."){
            steps{
                script{
                    echo 'Making the virtual environment...'
                    sh '''
                    python -m venv ${VENV_DIR}
                    . ${VENV_DIR}/bin/activate
                    pip install --upgrade pip
                    pip install -e .
                    pip install dvc
                    '''
                }
            }
        }


        stage('DVC Pull'){
            steps{
                withCredentials([file(credentialsId:'gcp-key', variable: 'GOOGLE_APPLICATION_CREDENTIALS')]){
                    script{
                        echo 'DVC Pull ...'
                        sh '''
                        . ${VENV_DIR}/bin/activate
                        dvc pull
                        '''
                    }
                }

            }
        }
    }
}