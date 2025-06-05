#!groovy
import groovy.json.JsonOutput

node {
        checkoutSource()
        build()
        allTests()
        createRelease("${env.GITHUB_ACTION}-${env.GITHUB_SHA}")
}

def checkoutSource() {
  stage ('checkoutSource') {
    copyFilesToWorkSpace()
  }
}

def copyFilesToWorkSpace() {
  mysh "cp -r /github/workspace/* $WORKSPACE"
}

def build () {
    stage ('Build') {
      sh './gradlew assemble'
    }
}

def allTests() {
    stage ('All tests') {

      sh './gradlew test'
    }
}
