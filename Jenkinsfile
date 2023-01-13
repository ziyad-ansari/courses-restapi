pipeline {
    agent { label 'agent7' }
    triggers { 
        pollSCM ('* * * * *')
        }
    stages {
        stage('SCM') {
            steps {
                git branch: 'dev',
                    url: 'https://github.com/ziyad-ansari/courses-restapi.git'
            }
        }
        stage('image build') {
            steps {
                sh "docker image build -t ansziyad5/courses:dev-$env.BUILD_ID ."
            }
        }
        stage('image deploy to registry') {
            steps {
                sh "docker image push ansziyad5/courses:dev-$env.BUILD_ID"
            }
        }
        stage('deploy on k8s') {
            steps {
                sh "cd deployments/courses/overlays/dev && kustomize edit set image courses=ansziyad5/courses:dev-$env.BUILD_ID"
                sh 'kubectl apply -k deployments/courses/overlays/develop'
            }
        }
    }
}