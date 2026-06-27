pipeline {
    agent {
        node {
            label 'maven'
        }
    }

    stages {
        stage('clone-code') {
            steps {
                git branch: 'main', 
                url: 'https://github.com/divyani2898/tweet-trend-new.git'
            }
        }
    }
}
