pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                bat '''
                git checkout master
                git pull
                '''
            }
        }
        stage('Sync to GitHub') {
            steps {
                bat '''
                echo %JAVA_HOME%
                cd
                cd appian-adm-versioning-client-2.5.9
                if %action% == addContents
                  version-application -action %action% -vc_username %git_username% -vc_password %git_password% -commit_message %commit_message% -application_path "%application_path%" -local_repo_path %local_repo_path% -repo_url %git_repo_url% -branch_name %git_branch_name%
                '''
            }
        }
        stage('Importing Application') {
            steps {
                bat '''
                cd appian-adm-import-client-2.5.9
                cd
                deploy-application.bat -username %appian_username% -password %appian_pwd% -url %target_environment% -application_path "%application_path%"
                '''
            }
        }
  }
}
