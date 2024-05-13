pipeline {
    agent any
    tools {
        maven "MAVEN3"
        jdk "OracleJDK8"
    
    }

    environment {
        SNAP_REPO = 'Aprofile-snapshot'
        NEXUS_USER = 'admin'
        NEXUS_PASS = 'admin123'
        RELEASE_REPO = 'Aprofile-release'
        CENTRAL_REPO = 'apro-maven-central'
        NEXUSIP = '172.31.10.199'
        NEXUSPORT - '8081'
        NEXUS_GRP_REPO = 'apro-maven-group'
        NEXUS_LOGIN = 'nexuslogin'
    }

    stages {
        stage ('Build'){
            steps {
                sh 'mvn -s settings.xml -Dskiptests install'
            }
        }
    }
}