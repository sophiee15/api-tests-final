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
    sh "docker build -t sophie14/python-greetings-app:latest ."

    echo "Pushing image to Docker Hub.."
    sh "docker push sophie14/python-greetings-app:latest"
}

def deploy(String environment) {
    echo "Deployment triggered on ${environment} env..."
    String lowerCaseEnv = environment.toLowerCase()

    sh "docker compose up -d python-greetings-app-${lowerCaseEnv}"
    sh "docker compose rm python-greetings-app-${lowerCaseEnv}"
    sh "docker compose up -d python-greetings-app-${lowerCaseEnv}"
}

def runApiTests(String environment) {
    echo "Running API tests on ${environment} env..."
    sh "docker pull sophie14/python-greetings-app"
    sh "docker run --network=host --rm sophie14/python-greetings-app:latest run greetings greetings_${environment}"
}
