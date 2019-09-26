pipeline {

    agent any

    stages {

        stage ('Build') {
            steps {
                withMaven(maven: 'maven_3_5_4') {
                    sh 'mvn clean package'
                }
            }
        }

        stage ('Deploy') {
            steps {
                withCredentials([[$class            : 'UsernamePasswordMultiBinding',
                                  credentialsId     : 'PCF_LOGIN',
                                  usernameVariable  : 'USERNAME',
                                  passwordVariable  : 'PASSWORD']]) {
                    sh '/usr/local/bin/cf login -a https://api.run.pivotal.io -u $USERNAME -p PASSWORD'
                }
            }
        }

    }

}