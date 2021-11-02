pipeline {
    agent { label 'ol8' }
    environment {
        version_prefix = "1.0.0"
        version_number = VersionNumber([versionNumberString: '-${BUILD_YEAR}${BUILD_MONTH,XX}${BUILD_DAY,XX}${BUILDS_TODAY_Z,XX}', versionPrefix: "${version_prefix}"])
        found_tag = "false"
        tag_value = "v${version_prefix}"
    }
    stages {
        stage('Echo environment') {
            steps {
                sh 'env|sort'
            }
        }
        stage('Look for tag') {
            when {
                tag pattern: "${tag_value}", comparator: "EQUALS"
            }
            steps {
                script {
                    found_tag = "true"
                }
            }
        }
        stage('Echo found_tag') {
            steps {
                echo "Found tag ${tag_value} is ${found_tag}"
            }
        }
    }
}
