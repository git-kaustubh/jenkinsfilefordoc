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
				sh "systemctl start docker"
				sh "docker stop 23q1 23q2 23q3"
				sh "docker system prune -a -f"
				sh "rm -rf /mnt/project/*"
				dir("/mnt/project/23Q1"){
					sh "git clone https://github.com/git-kaustubh/assignment-1.git -b 23Q1"
					sh "chmod 777 /mnt/project/23Q1/assignment-1/index.html"
				}
				dir("/mnt/project/23Q2"){
					sh "git clone https://github.com/git-kaustubh/assignment-1.git -b 23Q2"
					sh "chmod 777 /mnt/project/23Q2/assignment-1/index.html"
				}
				dir("/mnt/project/23Q3"){
					sh "git clone https://github.com/git-kaustubh/assignment-1.git -b 23Q3"
					sh "chmod 777 /mnt/project/23Q3/assignment-1/index.html"
				}
			}
		}
		stage("parallel stages"){
			parallel{
				stage("stage-1"){
					steps{
					sh "docker run -itdp 80:80 --name 23q1 kaustubh1997/testimage1"
					sh "docker cp /mnt/project/23Q1/assignment-1/index.html 23q1:/usr/local/apache2/htdocs/" 
					}
				}
				stage("stage-2"){
					steps{
					sh "docker run -itdp 90:80 --name 23q2 kaustubh1997/testimage1"
					sh "docker cp /mnt/project/23Q2/assignment-1/index.html 23q2:/usr/local/apache2/htdocs/" 
					}
				}
				stage("stage-3"){
					steps{
					sh "docker run -itdp 8081:80 --name 23q3 kaustubh1997/testimage1"
					sh "docker cp /mnt/project/23Q3/assignment-1/index.html 23q3:/usr/local/apache2/htdocs/" 
					}
				}
			}
		}
		
	}
}
