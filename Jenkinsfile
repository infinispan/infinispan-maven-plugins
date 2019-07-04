#!/usr/bin/env groovy

pipeline {
    agent {
        label 'slave-group-normal'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    def mvnHome = tool 'Maven'
                    sh "${mvnHome}/bin/mvn clean install -DskipTests=true -Dmaven.test.failure.ignore=true"
                }
            }
        }
    }

    post {
        cleanup {
            // Remove all untracked files, ignoring .gitignore
            sh 'git clean -qfdx || echo "git clean failed, exit code $?"'
        }
    }
}
