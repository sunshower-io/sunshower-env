#!/usr/bin/env groovy

def majorVersion   = "1"
def minorVersion   = "0"
def buildNumber
def buildSuffix    = "Final"
def version        = "$majorVersion.$minorVersion"
def runSystemTests = false
def tasks= []

if (env.BRANCH_NAME == "master") {
    buildNumber = env.BUILD_NUMBER
    tasks = [
        "versions:set",
        "-DnewVersion=$majorVersion.$minorVersion.$buildNumber.$buildSuffix"
    ]
} else {
    buildNumber = "${env.BUILD_NUMBER}.${convertBranchName(env.BRANCH_NAME)}"
    gradleTasks = [
            "versions:set",
            "-DnewVersion=$buildNumber"

    ]
}

node('docker-registry') {
    stage 'Checkout'
    checkout scm

    timeout(time: 60, unit: 'MINUTES') {
        try {
            sh "mvn ${tasks.join(' ')} clean install deploy"
        } catch (Exception e) {
            error "Failed: ${e}"
            throw (e)
        } finally {
            junit allowEmptyResults: true, keepLongStdio: true, testResults: '**/build/test-results/**/*.xml'
        }
    }
}

def convertBranchName(String name) {
    return name.replaceAll('/', '_')
}
