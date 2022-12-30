pipeline {

    agent any
    tools {
        //NOTE: must have node plugin installed
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
                
                /*script {

                    dir("app") {

                        sh "npm version patch"
                        //update build version variable
                        env.BUILD_VERSION = readJSON(file: 'package.json').version
                    }
                }
                //verify version update
                echo "updated to new version ${BUILD_VERSION}"*/
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

                    withCredentials([usernamePassword(credentialsId: 'docker', passwordVariable: 'PASSWORD', usernameVariable: 'USER')]) {
                        sh "docker build -t makecake/mod-8-example-app:${BUILD_VERSION} ."
                        sh "echo $PASSWORD | docker login -u $USER --password-stdin"
                        sh "docker push makecake/mod-8-example-app:${BUILD_VERSION}"
                    }
                }             
            }
        }

        //commit version update in git repo
        stage('commit') {
            steps {
                //webhook test 2
                echo "comitting to git..."
                
                /*script {
                    withCredentials([usernamePassword(credentialsId: 'github-tok', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        
                        //NOTE: add ignore commiter strategy plugin to avoid build and push loops
                        sh 'git config --global user.name "jenkins"'
                        sh 'git config --global user.email "jenkins@example.com"'

                        sh 'git status'
                        sh 'git branch'
                        sh 'git config --list'
                        
                        //NOTE: use auth token instead of password
                        sh "git remote set-url origin https://${USER}:${PASS}@github.com/makexcake/jenkins-example-project.git"
                        sh "git add ."
                        sh 'git commit -m "auto version bump"'
                        sh 'git push origin HEAD:main'
                    }
                }*/
            }
        }
    }
}
