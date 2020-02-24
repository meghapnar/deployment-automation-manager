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
                cd appian-adm-versioning-client-2.5.9
                version-application -action addContents -vc_password ${vc_password}
                '''
            }
        }
        stage('Import Manager') {
            steps {
                bat '''
                cd appian-adm-import-client-2.5.9
                cd
                deploy-application.bat -password ${appian_pwd}
                '''
            }
        }
  }
}
