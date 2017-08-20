node {
    checkout scm

    gerrit.withServer("http://gerrit:8080/", "gerrit") {

        try {
            docker.image('gerritforge/play-sbt-8-jdk-alpine').inside {
                stage('Build') {
                    sh sbt('compile')
                }
                stage('Test') {
                    sh sbt('test')
                }
            }

            gerrit.review("Verified", 1, "It works !")
        } catch (e) {
            gerrit.review("Verified", -1, "Breaks the build ;-(")
            throw e
        }
    }

    logstashSend failBuild: true, maxLines: 1000
}

def sbt(target) {
    return "sbt -no-colors $target"
}