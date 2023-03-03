node('jenkins'){
    stage('vcs'){
        git url: 'https://github.com/tejaswini1811/spring-petclinic.git',
        branch: 'scripted'
    }
    stage('build'){
        sh './mvnw package'
    }
      
}
