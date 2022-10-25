pipeline {

    agent any

    tools {
        //assign node
        nodejs "node"
    }

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
                        def versionFile = readJSON file: 'package.json'
                        def version = versionFile.version
                        env.BUILD_VERSION = $version
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

                dir ('app') {
                    //test the app according to README instructions
                    script {
                        sh "npm install"
                        sh "npm run test"
                    }
                }
            }
        }

        //build
        stage('build') {
            steps {

                echo "building and pushing to repo..."
                
                //build and push
                script {

                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'PASSWORD', usernameVariable: 'USER')]) {
                        sh "docker build -t makecake/mod-8-example-app:0.0.1 ."
                        sh "echo $PASSWORD | docker login -u $USER --password-stdin"
                        sh "docker push makecake/mod-8-example-app:0.0.1"
                    }
                }
                
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
