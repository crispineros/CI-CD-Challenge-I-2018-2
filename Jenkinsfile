pipeline {
    agent any
        stages {
            stage('Prepare') {
                steps {
                    echo 'Preparing..'
                    sh 'rm -rf CI-CD-Challenge-I-2018-2 ; git clone  https://github.com/crispineros/CI-CD-Challenge-I-2018-2 CI-CD-Challenge-I-2018-2'
                }
            }

            stage('Build') {
                steps {
                    echo 'Building..'
                    sh 'cd CI-CD-Challenge-I-2018-2 ;docker build . -t crispineros/image:1 '

                }
            }

            stage('Test') {
                steps {
                    echo 'Testing..'
                    sh 'docker run --name contenedor -d crispineros/image:1 npm test'

                }
            }

            stage('Push') {
                steps {
                    echo 'Clean & Push'
                    sh 'docker rm -f contenedor ; docker login -u crispineros -p cristian14 ; docker push crispineros/image:1 ; docker rmi -f crispineros/image:1 '

                }
            }

            stage('Deploy') {
                steps {
                    echo 'Deploy'
                    sh 'docker pull crispineros/image:1 ; docker run --name contenedor -d -p 9000:9000 crispineros/image:1 npm start'
                   input "Presione una tecla para detener el servidor."
                   sh 'docker stop contenedor; docker rm -f contenedor ; docker rmi -f crispineros/image:1'

                }
            }



        }
}
