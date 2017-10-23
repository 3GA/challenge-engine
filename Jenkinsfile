#!groovy

pipeline {
    agent {
        label 'win-test'
    }

    stages {
        // pulls down locally the sources for the component
        stage('checkout') {
            steps {
                checkout scm
            }
        }

        // Install the bower dependencies of the component
        stage('install dependencies') {
            steps {
                script {
                    sh "npm i"
                    sh "bower i"
                }
            }
        }

        // Lints, and tests the component
        stage('test') {
            steps {
                script {
                    sh "npm test"
                    junit allowEmptyResults: true, testResults: 'wct.xml'
                }
            }
        }
    }

    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }
}