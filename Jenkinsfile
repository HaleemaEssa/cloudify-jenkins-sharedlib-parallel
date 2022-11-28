//@Library("shared-library") _
pipeline {
  environment {
        DOCKERHUB_CREDENTIALS=credentials('haleema-dockerhub')
    }
  agent none
  stages {
    stage('Login to Dockerhub') {
      agent {label 'local'}
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        } 
    stage('cfy-Upload Blueprint') {
      agent {label 'local'}
            steps {
              git branch: 'main', url: 'https://github.com/HaleemaEssa/displayblueprintresuslt.git'
              sh 'cat upload-blueprint.txt'
              sleep(time: 1, unit: "SECONDS")
            }
        }
    stage('cfy-Create Deployment') {
      agent {label 'local'}
            steps {
              git branch: 'main', url: 'https://github.com/HaleemaEssa/displayblueprintresuslt.git'
              sh 'cat create-deployment.txt'
	      sleep(time: 1, unit: "SECONDS")

            }
        }
    stage('cfy-Start Execution') {
      agent {label 'local'}
            steps {
              git branch: 'main', url: 'https://github.com/HaleemaEssa/displayblueprintresuslt.git'
              sh 'cat start-execution.txt'
            }
        }
	stage('Data Transfering b/w RPi & Edge') {
	parallel {
	       stage('dht-sensor') {
		   options {
                timeout(time: 20, unit: "SECONDS")
            }
          agent {label 'linuxslave1'}
          steps {
             script { 
            try {
            sh 'echo "dht-sensor-task" '
            //git branch: 'main', url: 'https://github.com/HaleemaEssa/first_jenkins_project.git'
	    //git branch: 'main', url: 'https://github.com/HaleemaEssa/rpi-blynk.git'
            //sh 'docker build -t haleema/docker-rpi:latest .'
            //dockerBuild("haleema/docker-rpi:latest")
	    sh 'docker run --privileged -t haleema/docker-rpi-dht'
            sleep(time: 3, unit: "SECONDS")
            //sh 'docker run --privileged -t haleema/docker-rpi'
            //dockerRunPi("haleema/docker-rpi")
	    //dockerRunPi("haleema/docker-rpi-blynk")
            sleep(time: 2, unit: "SECONDS")
               } catch (Throwable e) {
                        echo "Caught ${e.toString()}"
                        currentBuild.result = "SUCCESS" //currentBuild.result = 'SUCCESS'
                    }
          }
	  }
	  
        }//stage
	      
	      
        stage('flame-sensor') {
		   options {
                timeout(time: 20, unit: "SECONDS")
            }
          agent {label 'linuxslave1'}
          steps {
             script { 
            try {
            sh 'echo "flame-sensor-tasks" '
            //git branch: 'main', url: 'https://github.com/HaleemaEssa/first_jenkins_project.git'
	    //git branch: 'main', url: 'https://github.com/HaleemaEssa/rpi-blynk.git'
            //sh 'docker build -t haleema/docker-rpi:latest .'
            //dockerBuild("haleema/docker-rpi:latest")
	    sh 'docker run --privileged -t haleema/docker-rpi-flame'
            sleep(time: 3, unit: "SECONDS")
            //sh 'docker run --privileged -t haleema/docker-rpi'
            //dockerRunPi("haleema/docker-rpi")
	    //dockerRunPi("haleema/docker-rpi-blynk")
            sleep(time: 2, unit: "SECONDS")
               } catch (Throwable e) {
                        echo "Caught ${e.toString()}"
                        currentBuild.result = "SUCCESS" //currentBuild.result = 'SUCCESS'
                    }
          }
	  }
	  
        }//stage
	stage('sound-sensor') {
		   options {
                timeout(time: 20, unit: "SECONDS")
            }
          agent {label 'linuxslave1'}
          steps {
             script { 
            try {
            sh 'echo "sound-sensor-tasks" '
            //git branch: 'main', url: 'https://github.com/HaleemaEssa/first_jenkins_project.git'
	    //git branch: 'main', url: 'https://github.com/HaleemaEssa/rpi-blynk.git'
            //sh 'docker build -t haleema/docker-rpi:latest .'
            //dockerBuild("haleema/docker-rpi:latest")
	    sh 'docker run --privileged -t haleema/docker-rpi-sound'
            sleep(time: 3, unit: "SECONDS")
            //sh 'docker run --privileged -t haleema/docker-rpi'
            //dockerRunPi("haleema/docker-rpi")
	    //dockerRunPi("haleema/docker-rpi-blynk")
            sleep(time: 2, unit: "SECONDS")
               } catch (Throwable e) {
                        echo "Caught ${e.toString()}"
                        currentBuild.result = "SUCCESS" //currentBuild.result = 'SUCCESS'
                    }
          }
	  }
	  
        }//stage
	}
	}
	
	
	
    stage('Data Transfering b/w RPi & Edge') {
     // parallel {
	       stage('On-RPI') {
	       parallel {
		   options {
                timeout(time: 30, unit: "SECONDS")
            }
          agent {label 'linuxslave1'}
	  stage ('dht-sensor')
          steps {
             script { 
            try {
            sh 'echo "send-data" '
            //git branch: 'main', url: 'https://github.com/HaleemaEssa/first_jenkins_project.git'
	    git branch: 'main', url: 'https://github.com/HaleemaEssa/rpi-blynk.git'
            //sh 'docker build -t haleema/docker-rpi:latest .'
            //dockerBuild("haleema/docker-rpi:latest")
	    //dockerBuild("haleema/docker-rpi-blynk:latest")
            sleep(time: 3, unit: "SECONDS")
            //sh 'docker run --privileged -t haleema/docker-rpi'
            //dockerRunPi("haleema/docker-rpi")
	    //dockerRunPi("haleema/docker-rpi-blynk")
	    //sh 'docker run --privileged -t haleema/docker-rpi-dht'
	    //sh 'docker run --privileged -t haleema/docker-rpi-flame'
	    //sh 'docker run --privileged -t haleema/docker-rpi-soung'
  	    sleep(time: 3, unit: "SECONDS")
	    sh 'docker kill $(docker ps -q)'
	     sleep(time: 3, unit: "SECONDS")
      sh 'docker run --privileged -t haleema/docker-rpi-blynk'
            sleep(time: 4, unit: "SECONDS")
               } catch (Throwable e) {
                        echo "Caught ${e.toString()}"
                        currentBuild.result = "SUCCESS" //currentBuild.result = 'SUCCESS'
                    }
          }
	  }
	  
        }//stage
	      
	      
        stage('Receive Data') {
		options {
                timeout(time: 30, unit: "SECONDS")
            }
   
          agent {label 'local'}
        
          steps {
            script { 
            try {
            sh 'echo "edge1"'
            git branch: 'main', url: 'https://github.com/HaleemaEssa/jenkins-edge-rec.git'
            //sh 'docker build -t haleema/docker-edge1:latest .'
            //dockerBuild("haleema/docker-edge1:latest")  
            echo "Started stage A"
            sleep(time: 3, unit: "SECONDS")
            sh 'docker run -v "${PWD}:/data" -t haleema/docker-edge1'
            //dockerRun("haleema/docker-edge1")
           // sleep(time: 2, unit: "SECONDS")
               } catch (Throwable e) {
                        echo "Caught ${e.toString()}"
                        currentBuild.result = "SUCCESS" 
                      //  sh 'nano data.csv'             
                    }
                

          }//script
        }//step
      }//stage
	//}//parallel
//}//stage
    
    stage('Data Preprocessing') {
          agent {label 'local'}
          steps {
            sh 'echo "Data Preprocessing"'
            git branch: 'main', url: 'https://github.com/HaleemaEssa/jenkins-edge-proc.git'
            //sh 'docker build -t haleema/docker-edge3:latest .'
            //dockerBuild("haleema/docker-edge3:latest")
            //sh 'sleep 10'
            //sh 'docker stop  haleema/docker-edge1; docker rm  haleema/docker-edge1'
            sh 'docker run -v "${PWD}:/data" -t haleema/docker-edge3'
            //sh 'sort -u head -n 1 /data/data.csv > data.csv'		  
            //dockerRun("haleema/docker-edge3")
            sleep(time: 3, unit: "SECONDS")
	  }
    }
	 stage('Sending pre-processed Data to Cloud') {
          agent {label 'local'}
          steps {	  
            sh 'echo "sending data to cloud based on Cloud AMQP"'
            git branch: 'main', url: 'https://github.com/HaleemaEssa/jenkins-edge-send.git'
            //sh 'docker build -t haleema/docker-edge222:latest .'
            //dockerBuild("haleema/docker-edge222:latest")
            //sh 'sleep 10'
            //sh 'docker stop  haleema/docker-edge1; docker rm  haleema/docker-edge1'
            sh 'docker run -v "${PWD}:/data" -t haleema/docker-edge222'
            //dockerRun("haleema/docker-edge222")

          }
        } 
       
    stage('Receiving Data in Cloud VM') {
           options {
                timeout(time: 60, unit: "SECONDS")
            }     
          agent {label 'server'} //server or aws
          steps {
            script { 
            try {
            sh 'echo "cloud" '
            git branch: 'main', url: 'https://github.com/HaleemaEssa/jenkins-cloud.git' //, credentialsId: 'cloudifyjenkins'
            //sh 'docker build -t haleema/docker-cloud:latest .'
            //dockerBuild("haleema/docker-cloud:latest")
            sh 'docker run -v "${PWD}:/data" -t haleema/docker-cloud'
            //dockerRun("haleema/docker-cloud")
            sleep(time: 2, unit: "SECONDS")
              } catch (Throwable e) {
                        echo "Caught ${e.toString()}"
                        currentBuild.result = "SUCCESS" 
                        //sh 'nano data.csv'             
                    }
            } 
          }
        }
    stage('On-Cloud-visulization') {
          agent {label 'server'} //server or aws
      steps {
            sh 'echo "cloud-visualization" '
            git branch: 'main', url: 'https://github.com/HaleemaEssa/jenkins-cloud-visualization.git'
            //sh 'docker build -t haleema/docker-cloud2:latest .'
            //dockerBuild("haleema/docker-cloud2:latest")
            sh 'docker run -v "${PWD}:/data" -t haleema/docker-cloud2'
            //dockerRun("haleema/docker-cloud2")
            
          }
        }
  }
     
    }
