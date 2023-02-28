pipeline{
	agent{
		label{
			label "built-in"
		}
	}
	stages{
		stage("initial"){
			steps{
				sh "yum install git -y"
				sh "yum install docker -y"
				sh "service docker start"
				sh "docker system prune -a -f"
				sh "rm -rf /mnt/project/*"
				dir("/mnt/project/23Q1"){
					sh "git clone https://github.com/Suraj7710/indexfile.git -b 23Q1"
					sh "chmod 777 /mnt/project/23Q1/indexfile/index.html"
				}
				dir("/mnt/project/23Q2"){
					sh "git clone https://github.com/Suraj7710/indexfile.git -b 23Q2"
					sh "chmod 777 /mnt/project/23Q2/indexfile/index.html"
				}
				dir("/mnt/project/23Q3"){
					sh "git clone https://github.com/Suraj7710/indexfile.git -b 23Q3"
                                        sh "chmod 777 /mnt/project/23Q3/indexfile/index.html"
				}
			}
		}
		stage("parallel stages"){
			parallel{
				stage("stage-1"){
					steps{
					sh "docker run -itdp 80:80 --name 23Q1 suraj7710/testimage1"
					sh "docker cp /mnt/project/23Q1/indexfile/index.html 23Q1:/usr/local/apache2/htdocs/" 
					}
				}
				stage("stage-2"){
					steps{
					sh "docker run -itdp 90:80 --name 23Q2 suraj7710/testimage1"
					sh "docker cp /mnt/project/23Q2/indexfile/index.html 23Q2:/usr/local/apache2/htdocs/" 
					}
				}
				stage("stage-3"){
					steps{
					sh "docker run -itdp 8081:80 --name 23Q3 suraj7710/testimage1"
					sh "docker cp /mnt/project/23Q3/indexfile/index.html 23Q3:/usr/local/apache2/htdocs/"
					}
			}
		}
		
	}
}
}
