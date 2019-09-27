pipeline {

    agent any

    stages {

        stage ('Build') {
            steps {
                withMaven(maven: 'maven3.5.4') {
                    bat 'mvn clean package'
                }
            }
        }

        stage ('Deploy') {
            steps {
                withCredentials([[$class            : 'UsernamePasswordMultiBinding',
                                  credentialsId     : 'PCF_LOGIN',
                                  usernameVariable  : 'USERNAME',
                                  passwordVariable  : 'PASSWORD']]) {
                    echo '$USERNAME $PASSWORD'
                    bat 'cf login -a https://api.run.pivotal.io -u $USERNAME -p $PASSWORD'
                }
            }
        }

    }

}