pipeline {
    agent any
    environment {
        version_prefix = "1.0.6"
        is_release = "false"
        found_tag = "false"
        github_url = "https://github.com/robertpatrick/jenkins-tag-test.git"
        github_creds = "fa369a2b-8c50-43ea-8956-71764cbcbe3d"
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
                git url: "${github_url}", credentialsId: "${github_creds}", branch: "${branch}"
            }
        }
        stage('Look for tag') {
            when {
                tag pattern: "v1.0.6", comparator: "EQUALS"
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
