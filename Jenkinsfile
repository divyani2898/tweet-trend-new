pipeline {
    agent {
        node {
            label 'maven'
        }
    }

    environment{
        PATH="/opt/apache-maven-3.9.11/bin:$PATH"
        IMAGE_NAME = "divyani2898/tweet-app"
        IMAGE_TAG = "2.1.2"

    }


    stages {

        stage('Build') {
            steps {
                sh '''
                export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
                export PATH=$JAVA_HOME/bin:$PATH

                java -version
                mvn clean deploy -Dmaven.test.skip=true

                '''
            }
        }


        stage("test"){
            steps{
                echo "----------- unit test started ----------"
                sh 'mvn surefire-report:report'
                 echo "----------- unit test Complted ----------"
            }
        }
               stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:$IMAGE_TAG .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-hub-cred',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {

                    sh '''
                    echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                    docker push $IMAGE_NAME:$IMAGE_TAG
                    
                    '''
                }
            }
        }

        stage("deploy"){
            steps{
                script{
                    sh './deploy.sh'
                }
            }
        }



        

        

    }
}
