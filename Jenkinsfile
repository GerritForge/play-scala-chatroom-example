#!/bin/env groovy

node {
    checkout scm

    stage('Build') {
        sh sbt('compile')
    }

    stage('Test') {
        sh snt('test')
    }
}

def sbt(target) {
    return "sbt -no-colors $target"
}