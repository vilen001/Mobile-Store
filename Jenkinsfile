pipeline{
    agent any
    stages{
        stage ('checkout the code from SCM'){
            steps{
                echo 'checkout the code'
            }
        }
        stage ('Build the project'){
            steps{
                echo 'building the project'
                sh 'mvn clean install -DskipTests'
            }
        }
        stage('Sonarqube'){
             steps{
                 echo 'Sonar Codequality'
                  sh ''' mvn clean verify sonar:sonar \
                            -Dsonar.projectKey=Mobilestore \
                            -Dsonar.host.url=http://20.77.168.249:9000 \
                            -Dsonar.login=sqp_5216990870fbf5e9487e3d3e3387c20c77e254a9 '''
            }
        }
         stage('building the docker image'){
             steps{
                 echo 'Docker image build'
                  sh 'docker build -t mobilestore .'
            }
        }
        stage('Deploy to dev'){
             steps{
                 echo "Deploying to dev environment"
                  sh 'docker rm -f mobile || true'
                   sh 'docker run -d --name=mobile -p 8099:8099 mobilestore'
            }
        }
    }
}