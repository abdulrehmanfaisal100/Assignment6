pipeline {
    agent any

    stages {
        stage('Display Node Name') {
            steps {
                script {
                    def nodeName = env.NODE_NAME
                    echo "The current node name is: ${nodeName}"
                }
            }
        }

        // Add more stages as needed
    }
    
    // Post-build actions, notifications, etc.
}
