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
                archiveArtifacts artifacts: '**/spring-petclinic-*.jar'
                junit testResults: '**/TEST-*.xml'
            }

        }
    }
}