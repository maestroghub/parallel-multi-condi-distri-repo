pipeline{
	agent{
		label{
			label 'slave2'
		}
	}
	stages{
	stage('version-control'){
			steps{
				checkout scmGit(branches: [[name: '(main|develop|feature.*)']], extensions: [], userRemoteConfigs: [[credentialsId: 'maestrog-id', url: 'https://github.com/maestroghub/multibranchrepo2.git']])
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