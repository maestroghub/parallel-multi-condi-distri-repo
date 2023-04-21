pipeline{
	agent{
		label{
			label 'slave2'
		}
	}
	stages{
	stage('version-control'){
			steps{
				checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-id', url: 'https://github.com/etechDevops/jenkins-parallel-job.git']]])
			}
		}
		stage('system-resources-check'){
			steps{
				sh "lscpu"
			}
		}
		stage('parallel-job'){
			parallel{
				stage('sub-job1'){
					steps{
						sh 'uptime'
					}
				}
			}
		}
		stage('codebuild'){
            agent{
                label{
                    label 'slave1'
                }
            }
            steps{
                sh 'date'
                sh 'cal'
            }
        }
		stage('parallel2-job'){
			parallel{
				stage('sub-job2'){
					steps{
						sh 'cat /etc/passwd'
					}
				}
			}
		stage('conditional-build'){
			when{
				branch 'feature'
			}
			steps{
				sh 'id ubuntu'
			}
        }
	}
}