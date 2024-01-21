pipeline{
        agent {label 'Dev-Node'}
            stages{
                stage('Code'){
                    steps{
                        git url: 'https://github.com/SantoshMorla/Nodejs_Signup_login_form.git'
                    }
                }
                
                stage('Build and Test'){
                    steps {
                        sh 'docker build . -t devsantosh03/node-signup-form-app:latest'
                    }
                }
                stage('Logging and Push'){
                    steps {
                        echo"Logging and pushing to DockerHub"
                        
						withCredentials([usernamePassword(credentialsId :'dockerhub',passwordVariable:'dockerhubPassword',usernameVariable:'userName')]){
                            sh "docker login -u ${env.userName} -p ${env.dockerhubPassword}"
                            sh "docker push devsantosh03/node-signup-form-app:latest"
                            
                        }
                    }
                }
                stage('Deploying'){
                    steps{
                      sh 'docker-compose down && docker-compose up -d' 
			echo"code successfully completed...."

			    
                    }
                }
                 
    
            }    
        }
