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
                version-application -action addContents vc_username %git_username% -vc_password %git_password% -commit_message %commit_message% -application_path %application_path% -admin_console_path %admin_console_path% -local_repo_path %local_repo_path% -repo_url %git_repo_url% -branch_name %git_branch_name%
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
