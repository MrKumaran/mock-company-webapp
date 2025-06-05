node {
        build()
        allTests()
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
//hi