@Library('jenkinslib') _
def tools = new org.devops.tools()
String workspace = "/var/lib/jenkins/workspace/my_temp"

pipeline {
    agent { node {
			label "master"
			customWorkspace "${workspace}"
		}
	}
	
	options {
		timestamps()
		skipDefaultCheckout()
		disableConcurrentBuilds()
		timeout(time: 1, unit: "HOURS")
		
	}
	

    stages {
        stage('GetCodeFromGit') {
            steps {
                timeout(time: 5, unit: "MINUTES"){
					script{
						println("获取代码")
						tools.PrintMsgWithColor("Pull code from git warehouse successful", "blue")
						// sh "printenv"
					}
				}
            }
        }
		
        stage('Build') {
            steps {
                timeout(time: 20, unit: "MINUTES"){
					script{
						println("应用打包")
						tools.PrintMsgWithColor("Pack the code successful", "red")
					}
				}
            }
        }	
		
        stage('Code Scan') {
            steps {
                timeout(time: 30, unit: "MINUTES"){
					script{
						println("代码扫描")
						//tools.printMsg("代码扫描成功")
						tools.PrintMsgWithColor("Scan code successful", "green")
					}
				}
            }
        }	
    }

	post{
		always {
			script{
					println("always")
				}
		}
		
		success {
			script{
					currentBuild.description += "\n 构建成功"
				}
		}

		failure {
			script{
					currentBuild.description += "\n 构建失败"
				}
		}	

		aborted {
			script{
					currentBuild.description += "\n 构建取消"
				}
		}			
	
	
	}
	
	
}
