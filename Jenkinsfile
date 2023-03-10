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
                  branch: 'jfrog'
            }
        }

        stage ('Artifactory configuration') {
            steps {
                rtServer (
                    id: "ARTIFACTORY_SPC",
                    url: 'https://tejaswini18.jfrog.io/artifactory',
                    credentialsId: 'JFROG'
                )

                rtMavenDeployer (
                    id: "MAVEN_DEPLOYER",
                    serverId: "ARTIFACTORY_SPC",
                    releaseRepo: 'libs-release-1',
                    snapshotRepo: 'libs-snapshot-1'
                )

                rtMavenResolver (
                    id: "MAVEN_RESOLVER",
                    serverId: "ARTIFACTORY_SPC",
                    releaseRepo: 'libs-release-1',
                    snapshotRepo: 'libs-snapshot-1'
                )
            }
        }

        stage ('Exec Maven') {
            steps {
                rtMavenRun (
                    tool: 'MVN_3.6.3', // Tool name from Jenkins configuration
                    pom: 'pom.xml',
                    goals: 'clean install',
                    deployerId: "MAVEN_DEPLOYER",
                    resolverId: "MAVEN_RESOLVER"
                )
            }
        }

        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "ARTIFACTORY_SPC"
                )
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