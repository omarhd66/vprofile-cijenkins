pipeline {
    agent any
    tools {
        maven "maven3"
        jdk "oracleJDK8"
    }
    
    environment {
        SNAP_REPO = 'vprofile-snapshot'
	NEXUS_USER = 'admin'
	NEXUS_PASS = 'umer'
	RELEASE_REPO = 'vprofile-release'
	CENTRAL_REPO = 'vpro-maven-central'
	NEXUSIP = '172.31.87.206'
	NEXUSPORT = '8081'
	NEXUS_GRP_REPO = 'vpro-maven-group'
        NEXUS_LOGIN = 'nexuslogin'
    }

    stages {
        stage('Build'){
            steps {
                sh 'mvn -s settings.xml -DskipTests install'
            }
            post {
                success {
                    echo "Now Archiving."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage('Test'){
            steps {
                sh 'mvn -s settings.xml test'
            }

        }

        stage('Checkstyle Analysis'){
            steps {
                sh 'mvn -s settings.xml checkstyle:checkstyle'
            }
        }
    }
}