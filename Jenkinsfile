pipeline {

    agent any

    stages {

        //init stage
        stage('init') {
            steps {
                echo "initialising..."
            }
        }

        //increase version
        stage('version increment') {
            steps {
                echo "increasing version..."
            }
        }

        //test
        stage('test') {
            steps {
                echo "testing..."
            }
        }

        //build
        stage('build') {
            steps {
                echo "building and pushing to repo..."
                //build and push
            }
        }

        //commit version update in git repo
        stage('commit') {
            steps {
                echo "comitting to git..."
            }
        }
    }
}
