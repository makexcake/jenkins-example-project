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
                
                script {

                    dir("app") {
                        sh "npm version patch"
                        //update build version variable
                        env.BUILD_VERSION = sh (script: """cat package.json | grep version | cut -d " " -f4 | grep -o '".*"' | sed 's/"//g' """, returnStdout: true)
                    }
                }
                //verify version update
                echo "updated to new version ${BUILD_VERSION}"
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
