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
        NEXUS_HOST = '172.31.37.76'
        NEXUS_PORT = '8081'
        NEXUS_USER = 'admin'
        NEXUS_PASS = 'admin123'
        APP_DIR = 'simple-java-maven-app'
        SONARSERVER='sonarserver'
        SONARSCANNER='sonarscanner'
    }

    stages {
        stage('Build') {
            steps {
                dir(env.APP_DIR) {
                    sh 'mvn -s ../settings.xml -DskipTests -U clean package'
                }
            }
            post {
                success {
                    dir(env.APP_DIR) {
                        echo 'Great! Now archiving the artifact.'
                        archiveArtifacts artifacts: '**/target/*.jar'
                    }
                }
            }
        }

        stage('Test') {
            steps {
                dir(env.APP_DIR) {
                    sh 'mvn -s ../settings.xml test'
                    sh 'mvn -s ../settings.xml verify'
                }
            }
        }
        stage('Code Quality') {
            steps {
                dir(env.APP_DIR) {
                    sh 'mvn  -s ../settings.xml checkstyle:checkstyle'
                }
            }
           
        }

  /*       stage('SonarQube Analysis'){
            environment{
                scannerHome = tool "${SONARSCANNER}"
            }
            steps{
                dir(env.APP_DIR){
                    withSonarQubeEnv("${SONARSERVER}") {
                        sh '''${scannerHome}/bin/sonar-scanner \
                        -Dsonar.projectkey=demo-app 
                        -Dsonar.projectName=demo-app
                        -Dsonar.projectVersion=1.0
                        -Dsonar.sources=src/main/java
                        -Dsonar.tests=src/test/java
                        -Dsonar.java.binaries=/target/classes
                        -Dsonar.junit.reportsPath=target/surefire-reports/
                        -Dsonar.jacoco.reportsPath=target/jacoco.exec
                        -Dsonar.java.checkstyle.reportsPaths=target/checkstyle-result.xml
                        
                        
                        
                        '''
                }
                }
            }
        } */
    }
}
