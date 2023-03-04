pipeline{
    agent{ label 'jenkins' }
    stages{
        stage('vcs'){
            steps{
              git url: 'https://github.com/tejaswini1811/spring-petclinic.git',
                  branch: 'declarative'
            }
        }
        stage('package'){
            steps{
                sh './gradlew assemble'
            }
        }
    }
}