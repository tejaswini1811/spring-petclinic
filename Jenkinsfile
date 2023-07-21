pipeline{
    agent{ label 'spc' }
    tools{ jdk 'jdk17'}
    stages{
        stage('vcs'){
            steps{
              git url: 'https://github.com/tejaswini1811/spring-petclinic.git',
                  branch: 'main'
            }
        }
        stage('build'){
            steps{
                sh './mvnw package'
            }
        }
        stage('deploy'){
            steps{
                sh 'java -jar target/*.jar'
            }
        }
    }
}