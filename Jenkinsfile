pipeline{
	agent{
		label{
			label 'slave2'
		}
	}
	stages{
		stage('1-version-control'){
			steps{
				checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-id', url: 'https://github.com/etechDevops/jenkins-parallel-job.git']]])
			}
		}
		stage('2-system-resources-check'){
			steps{
				sh "lscpu"
			}
		}
		stage('parallel-job1'){
			parallel{
				stage('system-check'){
					steps{
						sh 'uptime'
					}
				}
				stage('jenkins-user-check'){
					steps{
						sh 'id jenkins'
					}
				}
			}
		}
		stage{
			agent{
				label{
					label 'slave1'
				}
			}
        }
		stage{
			steps{
				sh 'date'
				sh 'cal'
			}
		}
		stage{
			parallel{
				stage('parallel-job2'){
					steps{
						sh 'cat /etc/passwd'
					}
				}
			}
		}
		stage{
			when{
				branch 'feature'
			}
			steps{
				sh 'id ubuntu'
			}
		}
	}
}