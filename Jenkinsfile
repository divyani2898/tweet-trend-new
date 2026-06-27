pipeline {
    agent {
        node {
            label 'maven'
        }
    }

    environment{
        PATH="/opt/apache-maven-3.9.11/bin:$PATH"

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

        stage('SonarQube analysis') {
            environment {
                scannerHome = tool 'valaxy-sonar-scanner'
            }

            steps {
                withSonarQubeEnv('valaxy-sonarqube-server') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }

    }
}