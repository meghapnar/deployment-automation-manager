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
              wrap([$class: 'BuildUser']) {
                bat '''
                echo "%JAVA_HOME%
                cd
                cd appian-adm-versioning-client-2.5.9
                if %action%==addContents goto :addContents
                if %action%==updateLocalRepo goto :updateLocalRepo
                if %action%==buildAllApps goto :buildAllApps
                if %action%==buildSingleApp goto :buildSingleApp
                if %action%==buildMultipleApps goto :buildMultipleApps
                    :addContents
                    version-application -action "%action%" -vc_username "%git_username%" -vc_password "%git_password%" -commit_message "%commit_message%"" %USERNAME%" -application_path "%application_path%" -local_repo_path "%local_repo_path%" -admin_console_path "%admin_console_path%" -ddl_path "%ddl_path%" -ddl_ds "%ddl_ds%" -repo_url "%git_repo_url%"-branch_name "%git_branch_name%
                    :updateLocalRepo
                    version-application -action "%action%" -vc_username "%git_username%" -vc_password "%git_password%" -commit_message "%commit_message%""%BUILD_USER_ID%" -application_path "%application_path%" -local_repo_path "%local_repo_path%" -admin_console_path "%admin_console_path%" -ddl_path "%ddl_path%" -ddl_ds "%ddl_ds%" -repo_url "%git_repo_url%"-branch_name "%git_branch_name%
                    :buildAllApps
                    version-application -action "%action%" -vc_username "%git_username%" -vc_password "%git_password%" -commit_message "%commit_message%""%BUILD_USER_ID%" -application_path "%application_path%" -local_repo_path "%local_repo_path%" -admin_console_path "%admin_console_path%" -ddl_path "%ddl_path%" -ddl_ds "%ddl_ds%" -repo_url "%git_repo_url%"-branch_name "%git_branch_name%"-package_path "%package_path%"-start_hash "%start_hash%"-end_hash "%end_hash%"-no_update "%no_update%
                    :buildSingleApp
                    version-application -action "%action%" -vc_username "%git_username%" -vc_password "%git_password%" -commit_message "%commit_message%""%BUILD_USER_ID%" -application_path "%application_path%" -local_repo_path "%local_repo_path%" -admin_console_path "%admin_console_path%" -ddl_path "%ddl_path%" -ddl_ds "%ddl_ds%" -repo_url "%git_repo_url%"-branch_name "%git_branch_name%"-application_name "%application_name%"-package_path "%package_path%"-uuid "%uuid%"-start_hash "%start_hash%"-end_hash "%end_hash%"-no_update "%no_update%
                    :buildMultipleApps
                    version-application -action "%action%" -vc_username "%git_username%" -vc_password "%git_password%" -commit_message "%commit_message%""%BUILD_USER_ID%" -application_path "%application_path%" -local_repo_path "%local_repo_path%" -admin_console_path "%admin_console_path%" -ddl_path "%ddl_path%" -ddl_ds "%ddl_ds%" -repo_url "%git_repo_url%"-branch_name "%git_branch_name%"-application_name "%application_name%"-package_path "%package_path%"-uuid "%uuid%"-start_hash "%start_hash%"-end_hash "%end_hash%"-no_update "%no_update%
                '''
                }
            }
        }
        stage('Importing Application') {
            steps {
                bat '''
                cd appian-adm-import-client-2.5.9
                cd
                deploy-application.bat -username "%appian_username%"-password "%appian_pwd%"-url "%target_environment%"-application_path "%application_path%"
                '''
            }
        }
  }
}
