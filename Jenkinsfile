node {
    checkout scm

    gerrit.withServer("http://gerrit:8080/", "gerrit") {
        def sha1 = sh(script: "git rev-parse HEAD", returnStdout: true).trim()
        gerrit.review("Verified", 1, "First feedback from Jenkins")
    }

    docker.image('gerritforge/play-sbt-8-jdk-alpine').inside {
        stage('Build') {
            sh sbt('compile')
        }
        stage('Test') {
            sh sbt('test')
        }

    }
}

def sbt(target) {
    return "sbt -no-colors $target"
}