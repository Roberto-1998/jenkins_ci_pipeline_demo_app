pipeline{
    agent any

    tools{
        maven : 'MAVEN3.9'
        jdk: 'JDK17'
    }

    environment{
       CENTRAL_REPO = 'demo-app-maven-central'
       SNAPSHOT_REPO = 'demo-app-snapshot'
       RELEASE_REPO = 'demo-app-release'
        NEXUS_HOST = '13.221.5.242'
        NEXUS_PORT = '8081'
        NEXUS_USER = 'admin'
        NEXUS_PASS = 'admin123'


    }


    stages{
        stage('Build'){
            steps{
                sh 'mvn -s settings.xml -DskipTests clean package'
            }
        }
    }
}