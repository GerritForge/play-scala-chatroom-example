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
                stage('Publish') {
                    sh sbt ('publish-local')
                }
            }

            gerrit.review("Verified", 1, "It works !")
        } catch (e) {
            gerrit.review("Verified", -1, "Breaks the build ;-(")
            throw e
        }
    }
}

def sbt(target) {
    return "sbt -no-colors $target"
}