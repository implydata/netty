pipeline {
    agent any

    environment {
        DOCKER_REPO="implydata.jfrog.io/docker-local"
        IMAGE="imply-docker/jfrog-mvn-java8:20201014.021741"
        RELEASE_BRANCH="3.10.6.Final-iap"
    }

    stages {
        stage('Pull Image') {
            steps {
                withDockerRegistry(url: "$DOCKER_REPO", credentialsId: "implydata.jfrog.io") {
                    sh "docker pull $DOCKER_REPO/$IMAGE"
                }
            }
        }

        stage ('Build') {
            steps {
                sh """
                    echo "mvn versions:set -B -DremoveSnapshot | true" > run.sh
                    echo "mvn clean install" >> run.sh
                    docker run -v ${WORKSPACE}/.m2:/root/.m2 -v ${WORKSPACE}:/app $DOCKER_REPO/$IMAGE bash run.sh
                """
            }
        }

        stage ('Publish') {
            when {
                branch "${RELEASE_BRANCH}"
            }
            steps {
                sh """
                    docker run -v ${WORKSPACE}/.m2:/root/.m2 -v ${WORKSPACE}:/app $DOCKER_REPO/$IMAGE jfrog rt mvn install
                """
            }
        }
    }
}
