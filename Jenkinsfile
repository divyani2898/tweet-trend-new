pipeline {
    agent {
        node {
            label 'maven'
        }
    }
    stage('Build') {
    steps {
        sh '''
        export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
        export PATH=$JAVA_HOME/bin:$PATH

        java -version
        mvn clean package
        '''
    }
}
    
    
}
