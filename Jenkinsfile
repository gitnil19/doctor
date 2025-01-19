pipeline {
    agent { label 'slave1' }

    stages {
        stage('SCM_Checkout') {
            steps {
               echo "Perform SCM Checkout"
			   git 'https://github.com/gitnil19/doctor.git'			   
            }
        }
        stage('Application Build') {
            steps {
                echo "Perform Application Build"
				sh 'mvn clean package'
            }
        }
        stage('Deploy to Test Server') {
            steps {
                script{
                   sshPublisher(publishers: [sshPublisherDesc(configName: 'Tomcat-Server', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '.', remoteDirectorySDF: false, removePrefix: 'target/', sourceFiles: 'target/*.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
                }
            }
        }
    }
}
