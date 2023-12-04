pipeline{
    agent{ label 'MAVEN'}
    options { 
        timeout(time: 30, unit: 'MINUTES') 
    }
    triggers { 
        pollSCM('* * * * *') 
    }
    stages{
        stage ('git') {
            steps{
                git url: 'https://github.com/prudhviraj123256/spring-petclinic-dummy.git',
                     branch: 'dev'
            }

        }
        stage('build') {
            steps{
                sh 'mvn clean package'
                
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/spring-petclinic-*.jar'
                    junit testResults: '**/TEST-*.xml'
                    mail subject: 'build stage succeded',
                         from: 'build@learningthoughts.io',
                         to: 'prudhviperuri@gmail.com',
                         body: "Refer to $BUILD_URL for more details"
                }
                failure {
                    mail subject: 'build stage failed',
                         from: 'build@learningthoughts.io',
                         to: 'prudhviperuri@gmail.com',
                         body: "Refer to $BUILD_URL for more details" 
                }
            }

        }
    }
}