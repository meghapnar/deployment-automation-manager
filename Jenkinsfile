pipeline {
    agent any
    stages {
        stage('Sync to GitHub') {
            steps {
                bat '''
                echo %JAVA_HOME%
                cd
                cd appian-adm-versioning-client-2.5.9
                if %action%==addContents goto :addContents
                if %action%==updateLocalRepo goto :updateLocalRepo
                if %action%==buildAllApps goto :buildAllApps
                if %action%==buildSingleApp goto :buildSingleApp
                if %action%==buildMultipleApps goto :buildMultipleApps
                :addContents
                if "%ddl_path%"=="" goto :addOnlyApp else goto :addAll
                :updateLocalRepo
                version-application -action "%action%" -vc_username "%git_username%" -vc_password "%git_password%" -commit_message "%commit_message% %git_username%" -application_path "%application_path%" -local_repo_path "%local_repo_path%" -admin_console_path "%admin_console_path%" -ddl_path "%ddl_path%" -ddl_ds "%ddl_ds%" -repo_url "%git_repo_url%" -branch_name "%git_branch_name%
                :buildAllApps
                version-application -action "%action%" -vc_username "%git_username%" -vc_password "%git_password%" -commit_message "%commit_message% %git_username%" -application_path "%application_path%" -local_repo_path "%local_repo_path%" -admin_console_path "%admin_console_path%" -ddl_path "%ddl_path%" -ddl_ds "%ddl_ds%" -repo_url "%git_repo_url%" -branch_name "%git_branch_name%" -package_path "%package_path%" -start_hash "%start_hash%" -end_hash "%end_hash%" -no_update "%no_update%
                :buildSingleApp
                version-application -action "%action%" -vc_username "%git_username%" -vc_password "%git_password%" -commit_message "%commit_message% %git_username%" -application_path "%application_path%" -local_repo_path "%local_repo_path%" -admin_console_path "%admin_console_path%" -ddl_path "%ddl_path%" -ddl_ds "%ddl_ds%" -repo_url "%git_repo_url%" -branch_name "%git_branch_name%" -application_name "%application_name%" -package_path "%package_path%" -uuid "%uuid%" -start_hash "%start_hash%" -end_hash "%end_hash%" -no_update "%no_update%
                :buildMultipleApps
                version-application -action "%action%" -vc_username "%git_username%" -vc_password "%git_password%" -commit_message "%commit_message% %git_username%" -application_path "%application_path%" -local_repo_path "%local_repo_path%" -admin_console_path "%admin_console_path%" -ddl_path "%ddl_path%" -ddl_ds "%ddl_ds%" -repo_url "%git_repo_url%" -branch_name "%git_branch_name%" -application_name "%application_name%"-package_path "%package_path%" -uuid "%uuid%" -start_hash "%start_hash%" -end_hash "%end_hash%" -no_update "%no_update%
                :addOnlyApp
                version-application -action "%action%" -vc_username "%git_username%" -vc_password "%git_password%" -commit_message "%commit_message% %git_username%" -application_path "%application_path%" -application_name "%application_name%" -local_repo_path "%local_repo_path%" -admin_console_path "%admin_console_path%" -uuid "%uuid%" -appian_objects_repo_path "%appian_objects_repo_path%" -repo_url "%git_repo_url%" -branch_name "%git_branch_name%"
                :addAll
                version-application -action "%action%" -vc_username "%git_username%" -vc_password "%git_password%" -commit_message "%commit_message% %git_username%" -application_path "%application_path%" -application_name "%application_name%" -local_repo_path "%local_repo_path%" -admin_console_path "%admin_console_path%" -ddl_path "%ddl_path%" -ddl_ds "%ddl_ds%" -flyway_path "%flyway_path%" -uuid "%uuid%" -appian_objects_repo_path "%appian_objects_repo_path%" -repo_url "%git_repo_url%" -branch_name "%git_branch_name%"
                '''
            }
        }
  }
}
