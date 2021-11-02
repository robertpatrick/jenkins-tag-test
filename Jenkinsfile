pipeline {
    agent any
    environment {
        version_prefix = "1.0.2"
        version_number = VersionNumber([versionNumberString: '-${BUILD_YEAR}${BUILD_MONTH,XX}${BUILD_DAY,XX}${BUILDS_TODAY_Z,XX}', versionPrefix: "${version_prefix}"])
        is_release = "false"
        found_tag = "false"
        github_url = "https://github.com/robertpatrick/jenkins-tag-test.git"
        branch = sh(returnStdout: true, script: 'echo $GIT_BRANCH | sed --expression "s:origin/::"')
    }
    stages {
        stage('Echo environment') {
            steps {
                sh 'env|sort'
            }
        }
        stage('Checkout') {
            steps {
                git url: "${github_url}", branch: "${branch}"
            }
        }
        stage('Look for tag') {
            when {
                tag "v1.0.2"
            }
            steps {
                script {
                    found_tag = "true"
                }
            }
        }
        stage('Look for release') {
            when {
                changelog '.*^\\[release\\].+$'
            }
            steps {
                script {
                    is_release = "true"
                }
            }
        }
        stage('Echo is_release') {
            steps {
                echo "Found tag v1.0.0 is ${found_tag}"
                echo "Found release marker is ${is_release}"
            }
        }
    }
}
