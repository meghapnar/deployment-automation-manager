pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                bat 'git checkout master'
            }
        }
        stage('Version Manager') {
            steps {
                bat '''
                echo $JAVA_HOME
                cd
                REM cd appian-adm-versioning-client-2.5.9
                REM version-application -action addContents -vc_password Its4megha
                '''
            }
        }
        stage('Import Manager') {
            steps {
                bat '''
                cd appian-adm-import-client-2.5.9
                cd
                deploy-application.bat -password a
                '''
            }
        }
  }
}
