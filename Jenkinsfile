pipeline {
    agent any

    environment {
        // Caminho do kubeconfig no Windows
        KUBECONFIG = 'C:\\Users\\leone\\.kube\\config'
    }

    stages {
        stage('Clonar Repositório') {
            steps {
                git 'https://github.com/leonelcostajunior/deploy_aws.git'
            }
        }

        stage('Aplicar Pod') {
            steps {
                bat """
                kubectl apply -f k8s\\meu-primeiro-pod.yaml
                kubectl get pods -o wide
                """
            }
        }

        stage('Aplicar Deployment') {
            steps {
                bat """
                kubectl apply -f k8s\\deploy-aws-deployment.yaml
                kubectl get deployments
                """
            }
        }

        stage('Aplicar Service') {
            steps {
                bat """
                kubectl apply -f k8s\\deploy-aws-service.yaml
                kubectl get svc
                """
            }
        }

        stage('Aplicar HPA') {
            steps {
                bat """
                kubectl apply -f k8s\\deploy-aws-hpa.yaml
                kubectl get hpa
                """
            }
        }
    }

    post {
        success {
            echo 'Pipeline CI/CD finalizado com sucesso!'
        }
        failure {
            echo 'Pipeline falhou!'
        }
    }
}
