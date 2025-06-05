#!groovy
import groovy.json.JsonOutput

node {
        checkoutSource()
        build()
        allTests()
}

def checkoutSource() {
  stage ('checkoutSource') {
    sh "cp -r /github/workspace/* $WORKSPACE"
  }
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
