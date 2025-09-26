def hasChanges(String path) {
    return !sh(script: "git diff --name-only HEAD~1 HEAD | grep '${path}' || true", returnStdout: true).trim().isEmpty()
}

pipeline {
    agent any

    stages {
        stage('Detect changes') {
            steps {
                script {
                    if (hasChanges('frontend/')) {
                        echo "Changes detected in frontend/"
                    } else {
                        echo "No changes in frontend/"
                    }

                    if (hasChanges('backend/')) {
                        echo "Changes detected in backend/"
                    } else {
                        echo "No changes in backend/"
                    }
            }
        }
        stage('Frontend change') {
            when {
                    changeset "**/frontend/**"
            }
            steps {
                echo "Frontend files have changed"
            }
        }
        stage('Backend change') {
            when {
                    changeset "**/backend/**"
            }
            steps {
                echo "Backend files have changed"
            }
        }
    }
}
