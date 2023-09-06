// pipeline {
//     agent{
//         label 'agent1'
//     }

//     stages {
//         stage('Display Node Name') {
//             steps {
//                 script {
//                     def nodeName = env.NODE_NAME
//                     echo "The current node name is: ${nodeName}"
//                 }
//             }
//         }

//         // Add more stages as needed
//     }
    
//     // Post-build actions, notifications, etc.
// }
pipeline {
  agent any
  stages {
    stage('Scan') {
      steps {
        withSonarQubeEnv(installationName: 'Sq1') { 
          sh './mvnw clean org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.0.2155:sonar'
        }
      }
    }
  }
}