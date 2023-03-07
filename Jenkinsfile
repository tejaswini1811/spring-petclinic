pipeline{
    agent{ label 'JDK_17' }
    tools{ jdk 'JDK_17_UBUNTU'}
    stages{
        stage('vcs'){
            steps{
              git url: 'https://github.com/tejaswini1811/spring-petclinic.git',
                  branch: 'sonar'
            }
        }
        stage('build'){
            tools { maven 'MVN_3.6.3'}
            steps{
                sh 'mvn package'
            }
        }
        stage('sonar analysis'){
            steps{
                  withSonarQubeEnv('SONAR_JENKINS'){
                    sh 'mvn clean package sonar:sonar -Dsonar.organization=springpetclinic1'
                  }
            }
        }
        stage('postbuild'){
            steps{
                archiveArtifacts artifacts :'**/target/*.jar',
                                onlyIfSuccessful : true
                junit testResults : '**/surefire-reports/TEST-*.xml'
            }
        }
    }
}