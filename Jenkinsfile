pipeline{
    agent{ label 'jenkins' }
    tools{ jdk 'JAVA_17_UBUNTU'}
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
        stage('mail'){
            steps{
                mail subject: 'jenkins spc',
                to: 'jenkins@gmail.com',
                body: 'hiiiii'
            }
        }
    }
}