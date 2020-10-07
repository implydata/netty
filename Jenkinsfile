pipeline {
    agent any
    environment {
        ECR="018895040333.dkr.ecr.us-east-1.amazonaws.com"
        IMAGE="imply-eng/jfrog-mvn-java8:20201009-033920"
    }
    stages {

        stage('Pull Image') {
            steps {
                withDockerRegistry([url: "https://$ECR", credentialsId: "ecr:us-east-1:aws"]) {
                    sh "docker pull $ECR/$IMAGE"
                }
            }
        }

        stage ('Build and Publish') {
            steps {
                sh """
                    echo "mvn versions:set -B -DremoveSnapshot | true" > run.sh
                    echo "jfrog rt mvn clean install" >> run.sh
                    docker run -v ${WORKSPACE}/.m2:/root/.m2 -v ${WORKSPACE}:/app $ECR/$IMAGE bash run.sh
                """
            }
        }
    }
}
