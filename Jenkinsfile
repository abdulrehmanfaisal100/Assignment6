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
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }
  stages {
    stage('Scan') {
      steps {
        withSonarQubeEnv(installationName: 'Sq1') { 
          sh './mvnw clean org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.0.2155:sonar'
        }
      }
    }
    stage('Build Docker Image') {
      steps {
          script {
              // Define the Dockerfile location
              def dockerfile = './Dockerfile'

              // Build the Docker image
              def customImage = docker.build("abdulrehman100/maven_image:latest", "-f ${dockerfile} .")

              // Push the image to a Docker registry (optional)
          }
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push abdulrehman100/maven_image'
      }
    }
    stage('Access EC2 and run application') {
      // agent {
      //   label 'agent1'
      // }
      steps {
        sh "ssh -o StrictHostKeyChecking=no -i ~/Important.pem ubuntu@54.80.126.41 'sudo docker pull abdulrehman100/maven_image'"
      }
    }
    stage('Deploying application on EC2') {
      steps {
        sh "ssh -o StrictHostKeyChecking=no -i ~/Important.pem ubuntu@54.80.126.41 'sudo docker run -p 8081:8081 -e PORT=8081 -d c29926acff4b'"
      }
    }
  }
}