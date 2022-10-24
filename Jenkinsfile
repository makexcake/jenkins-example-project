pipeline {

    agent any

    stages {

        //init stage
        stage('init') {
            steps {
                script{
                    echo "initiating"
                }
            }
        }

        //increase version
        stage('version increment') {
            steps {
                script {
                    "increasing version.."
                }
            }
        }

        //test
        stage('test') {
            steps {
                script {
                    echo "testing"
                }
            }
        }

        //build
        stage('build') {
            steps {
                script {
                    echo "building.."
                    //build and push to repo
                }
            }
        }

        //commit version update in git repo
        stage('commit') {
            script {
                echo "commiting to github"
            }
        }
    }
}
