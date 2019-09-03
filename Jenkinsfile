def image_repo
def image_tag
pipeline {
  agent {
    label 'master'
  }
  environment {
    GOPATH = "$WORKSPACE"
    GITHUB_COMMIT="$GIT_COMMIT"
    CHANGE_ID="$CHANGE_ID"
    BRANCH_NAME="$BRANCH_NAME"
    DIRECTORY="/mnt/home/adua/test_r"
  }

  stages {
    
    stage("First") {
     
      steps {
        script{
        def url="$GIT_URL"
        image_repo="docker.io/infobloxcto/siemserver"
        env.image_repo=image_repo
        image_tag="2018.21"
        env.image_tag=image_tag
        final git_repo = url.substring(url.lastIndexOf('/') + 1, url.length())
        echo git_repo
        env.GIT_REPO =git_repo
        echo env.GIT_REPO
        echo env.GITHUB_COMMIT
        echo env.CHANGE_ID
        echo env.BRANCH_NAME
        def IMAGE_NAMES_LIST="make show-image-name 2>/dev/null"
        def IMAGE_VERSION="make show-image-version"
        echo "repo1=infobloxcto/${IMAGE_NAMES_LIST}" 
        echo "tag1=${IMAGE_VERSION}"
        }

       }
  
    }    
    }
    
    stage("Build CVE job"){
      steps{
    
      build job: 'run_docker_image_cve_scan', parameters: [[$class: 'StringParameterValue', name: 'COMMIT_ID', value:env.GITHUB_COMMIT], [$class: 'StringParameterValue', name: 'GITHUB_REPO', value:env.GIT_REPO],[$class: 'StringParameterValue', name: 'CHANGE_ID', defaultValue:'',value:env.CHANGE_ID],[$class: 'StringParameterValue', name: 'repo', value:env.image_repo],[$class: 'StringParameterValue', name: 'tag', value:env.image_tag]]
      
   
      }
  }
} 
} 
