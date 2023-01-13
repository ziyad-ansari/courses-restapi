pipeline {
    agent { label 'agent7' }
    triggers { 
        pollSCM ('* * * * *')
        }
    stages {
        stage('SCM') {
            steps {
                git branch: 'dev',
                    url: 'https://github.com/ziyad-ansari/Project-StudentCoursesRestAPI.git'
            }
        }
        stage('image build') {
            steps {
                sh 'docker image build -t ansziyad5/courses:dev-$env.BUILD_ID .'
            }
        }
        stage('image deploy to registry') {
            steps {
                sh 'docker image push ansziyad5/courses:dev-$env.BUILD_ID'
            }
        }
    }
}