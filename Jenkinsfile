pipeline {
  agent {
     label 'ubuntu_docker_label'
  }
  
  parameters {
    string(name: 'image_repo', defaultValue: '', description: 'Docker image repo')
    string(name: 'image_tag', defaultValue: '', description: 'Docker image tag')
    string(name: 'github_repo', defaultValue: '', description: 'Github repo')
  }
  
  environment {
    image_repo = get_image_repo_from(params)
    image_tag = get_image_tag_from(params)
    upstream_github_repo = get_github_repo_from(params)
    upstream_execution_url = "$BUILD_URL"
    upstream_job_name = "$JOB_BASE_NAME"
    upstream_build_id = "$BUILD_ID"
    email_recipients = get_email_recipients(ownership)
  }

  stages {
    stage("Test Stage") {
      steps {
        sh "pwd"
        sh "ls -Alh"
      }
    }
  }
  
  post {
    always {
            cleanWs()
        }
  }
}
