#!/bin/env groovy

node {
    checkout scm

    docker.image('GerritForge/play-sbt-8-jdk-alpine').inside {

        stage('Build') {
            sh sbt('compile')
        }

        stage('Test') {
            sh snt('test')
        }
    }
}

def sbt(target) {
    return "sbt -no-colors $target"
}