
pipeline {

    agent {
        label 'docker-agent'
    }

    environment {
        APP_NAME = 'mon-application'
        APP_ENV = 'development'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Recuperation du code source'
                sh '''
                    echo "Job Jenkins : $JOB_NAME"
                    echo "Numero du build : $BUILD_NUMBER"
                    echo "Workspace : $WORKSPACE"
                    echo "Nom application : $APP_NAME"
                    echo "Environnement : $APP_ENV"
                '''
            }
        }

        stage('Build') {
            steps {
                echo "Construction de ${env.APP_NAME}"
                sh '''
                    mkdir -p build
                    echo "Application : $APP_NAME" > build/application.txt
                    echo "Environnement : $APP_ENV" >> build/application.txt
                    cat build/application.txt
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Execution des tests'
                sh '''
                    if [ -f build/application.txt ]; then
                        echo "Test : application presente - OK"
                    else
                        echo "Test : application absente - ECHEC"
                        exit 1
                    fi
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploiement de ${env.APP_NAME}"
                sh '''
                    mkdir -p deployment
                    cp build/application.txt deployment/
                    echo "Deploiement termine dans l environnement : $APP_ENV"
                '''
            }
        }
    }
}

