pipeline {
    agent any
    triggers {
        pollSCM('*/1 * * * *')  
    }
    stages {
        stage('building-docker-image') {
            steps {
                buildDockerImage()
            }
        }
        stage('deploy-dev') {
            steps {
                deploy("DEV")
            }
        }
        stage('test-dev') {
            steps {
                runApiTests("DEV")
            }
        }
        stage('deploy-stg') {
            steps {
                deploy("STG")
            }
        }
        stage('test-stg') {
            steps {
                runApiTests("STG")
            }
        }
        stage('deploy-prd') {
            steps {
                deploy("PRD")
            }
        }
        stage('test-prd') {
            steps {
                runApiTests("PRD")
            }
        }
    }
}

def buildDockerImage() {
    echo "Building Docker image.."
    sh "docker build -t sophie14/api-tests-final ."

    echo "Pushing image to Docker Hub.."
    sh "docker push sophie14/api-tests-final"
}

def deploy(String environment) {
    echo "Deployment triggered on ${environment} env..."
    String lowerCaseEnv = environment.toLowerCase()

    sh "docker compose up -d api-tests-final-${lowerCaseEnv}"
    sh "docker compose rm api-tests-final-${lowerCaseEnv}"
    sh "docker compose up -d api-tests-final-${lowerCaseEnv}"
}

def runApiTests(String environment) {
    echo "Running API tests on ${environment} env..."
    sh "docker pull sophie14/api-tests-final"
    sh "docker run --network=host --rm sophie14/api-tests-final run greetings greetings_${environment}"
}
