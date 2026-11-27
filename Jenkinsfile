
pipeline {

    agent {
        label 'docker-agent'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Recuperation du code source'
                sh '''
                    echo "Repertoire de travail :"
                    pwd

                    echo "Fichiers du projet :"
                    ls -la
                '''
            }
        }

        stage('Build') {
            steps {
                echo 'Construction de l application'
                sh '''
                    mkdir -p build

                    echo "Application construite par Jenkins" > build/application.txt

                    echo "Contenu du repertoire build :"
                    ls -l build

                    echo "Contenu du fichier genere :"
                    cat build/application.txt
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Execution des tests'
                sh '''
                    if [ -f build/application.txt ]; then
                        echo "Test 1 : fichier application present - OK"
                    else
                        echo "Test 1 : fichier application absent - ECHEC"
                        exit 1
                    fi

                    echo "Tous les tests sont passes."
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploiement de l application'
                sh '''
                    mkdir -p deployment
                    cp build/application.txt deployment/
                    echo "Application deployee avec succes."
                    ls -l deployment
                '''
            }
        }
    }
}

