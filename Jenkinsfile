pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from GitHub
                git 'https://github.com/Chandu3366/my-project.git'
            }
        }

        stage('Build') {
            steps {
                // Build the Maven project
                sh 'mvn clean install'
            }
        }

        /*stage('SonarQube') {
            steps {
                // Run SonarQube analysis
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar'
                }
            }
        }*/

        stage('Build Docker Image') {
            steps {
                // Build and tag Docker image
                sh 'docker build -t your-image:latest .'
            }
        }

        stage('Push Docker Image') {
            steps {
                // Push Docker image to a Docker registry
                withDockerRegistry([credentialsId: 'your-docker-credentials', url: 'https://your-docker-registry-url']) {
                    sh 'docker push your-image:latest'
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                // Deploy the application to Kubernetes
                withKubeConfig([credentialsId: 'your-kubeconfig-credentials']) {
                    sh 'kubectl apply -f your-kubernetes-manifest.yml'
                }
            }
        }
    }

    post {
        always {
            // Clean up any temporary resources, if required
            deleteDir()
        }
    }
}
