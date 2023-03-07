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
                sh 'mvn package'
            }
        }
        stage('sonar analysis'){
            steps{
                  withSonarQubeEnv('SONAR_JENKINS'){
                    sh 'mvn clean package org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.organization=tejaswini1811'
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