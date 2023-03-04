node('jenkins'){
    stage('vcs'){
        git url: 'https://github.com/tejaswini1811/spring-petclinic.git',
            branch: 'scripted'
    }
    stage('package'){
        tools {
            jdk 'JAVA-17-UBUNTU'
        }
    }
    stage('build'){
        sh './gradlew assemble'
    }
      
}
