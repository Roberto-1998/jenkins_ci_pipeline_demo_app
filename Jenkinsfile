pipeline {
    agent any

    tools {
        maven 'MAVEN3.9'
        jdk 'JDK21'
    }

    environment {
        CENTRAL_REPO = 'demo-app-maven-central'
        SNAPSHOT_REPO = 'demo-app-snapshot'
        RELEASE_REPO = 'demo-app-release'
        NEXUS_HOST = '13.221.5.242'
        NEXUS_PORT = '8081'
        NEXUS_USER = 'admin'
        NEXUS_PASS = 'admin123'
        APP_DIR = 'simple-java-maven-app'
    }

    stages {
        stage('Build') {
            steps {
                dir(env.APP_DIR){
                 sh 'mvn -s ../settings.xml -DskipTests clean package'
                }
            }
        }
    }
}
