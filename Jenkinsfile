pipeline{
    agent{ label 'jenkins' }
    tools{ jdk 'JDK-17-UBUNTU'}
    stages{
        stage('vcs'){
            steps{
              git url: 'https://github.com/tejaswini1811/spring-petclinic.git',
                  branch: 'declarative'
            }
        }
        stage('build'){
            steps{
                sh './gradlew assemble'
            }
        }
    }
}