pipeline {
    agent any
    stages {

        stage('Clone Repo') {
          steps {
            sh 'rm -rf dockertest1' 
            sh 'git clone https://github.com/KNarendra99599/dockertest1.git' 
            }
        }
       
        stage('Build Docker Image') {
          steps {
            sh 'cd /var/lib/jenkins/workspace/pipeline2/dockertest1'
            sh 'cp /var/lib/jenkins/workspace/pipeline2/dockertest1/* /var/lib/jenkins/workspace/pipeline2'
            sh 'docker build -t kasaragadda99599/pipelinetest:v1 .'
            }
        }

        stage('Push Image to Docker Hub') {
          steps {
            sh    'docker push kasaragadda99599/pipelinetest:v1'
            }
        }

        stage('Deploy to Docker Host') {
          steps {
            sh 'docker -H tcp://172.31.1.200:2375 stop webapp1'
            sh 'docker  -H tcp://172.31.1.200:2375 run --rm -dit --name webapp1 --hostname webapp1 -p 9000:80 kasaragadda99599/pipelinetest:v1'
            }

        }

        stage('Check WebApp Reachability'){
          steps {
            sh 'sleep 10s'
            sh 'curl http://ec2-3-236-197-193.compute-1.amazonaws.com:9000'
            }
        }

    }

}
