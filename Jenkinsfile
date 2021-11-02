pipeline {
    agent { label 'ol8' }
    environment {
        version_prefix = "1.0.0"
        version_number = VersionNumber([versionNumberString: '-${BUILD_YEAR}${BUILD_MONTH,XX}${BUILD_DAY,XX}${BUILDS_TODAY_Z,XX}', versionPrefix: "${version_prefix}"])
        is_release = "false"
    }
    stages {
        stage('Echo environment') {
            steps {
                sh 'env|sort'
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
                echo "Found release marker is ${is_release}"
            }
        }
    }
}
