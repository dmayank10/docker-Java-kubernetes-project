pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout the Git repository
                git branch: 'mayank', credentialsId: 'djkp', url: 'https://github.com/dmayank10/docker-Java-kubernetes-project.git'
            }
        }
        
        stage('Build') {
            steps {
                // Build using Maven
                sh 'mvn clean package'
            }
        }
        
        stage('Docker Build & Push') {
            steps {
                script {
                    // Build and tag Docker image
                    def imageName = "djkp:${env.BUILD_ID}"
                    docker.build(imageName, '.')

                    // Push Docker image to registry
                    docker.withRegistry(credentialsId: 'djkp', url: 'https://hub.docker.com/') {
                        docker.image(imageName).push()
                    }
                }
            }
        }
        
        // stage('Kubernetes Deploy') {
        //     steps {
        //         // Deploy to Kubernetes
        //         kubeConfig(
        //             credentialsId: 'kubeconfig-credentials-id',
        //             disableAutoRefresh: false,
        //             kubeconfigId: 'kubeconfig-id'
        //         )
        //         kubernetesDeploy(
        //             configs: 'path/to/kubernetes/deployment.yaml',
        //             enableConfigSubstitution: true
        //         )
        //     }
        // }
    }
}
