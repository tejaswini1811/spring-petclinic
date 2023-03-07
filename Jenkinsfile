pipeline{
    agent{ label 'JDK_17' }
    tools{
        jdk 'JDK_17_UBUNTU'
        maven 'MVN_3.6.3'  
    }
    stages{
        stage('vcs'){
            steps{
              git url: 'https://github.com/tejaswini1811/spring-petclinic.git',
                  branch: 'sonar'
            }
        }
        stage('build'){
            steps{
                mail subject: "Jenkins Build of ${JOB_NAME} with id ${BUILD_ID} is started",
                     body: "Use this URL ${BUILD_URL} for more info",
                     to: 'all@gmail.com'
                sh 'mvn package'
                mail subject: "Jenkins Build of ${JOB_NAME} with id ${BUILD_ID} is completed",
                     body: "Use this URL ${BUILD_URL} for more info",
                     to: 'all@gmail.com'
            }
        }
        stage('sonar analysis'){
            steps{
                mail subject: "Jenkins Build of ${JOB_NAME} with id ${BUILD_ID} is started sonar analysis",
                     body: "Use this URL ${BUILD_URL} for more info",
                     to: 'all@gmail.com'
                withSonarQubeEnv('SONAR_JENKINS'){
                sh 'mvn clean package sonar:sonar -Dsonar.organization=spc-jenkins -Dsonar.projectKey=spc-jenkins_petclinic'
                mail subject: "Jenkins Build of ${JOB_NAME} with id ${BUILD_ID} is completed sonar analysis",
                     body: "Use this URL ${BUILD_URL} for more info",
                     to: 'all@gmail.com'
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