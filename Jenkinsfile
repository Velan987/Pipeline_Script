pipeline {
    agent any
    stages {
		stage('Git-Checkout') {
			steps{
				git 'https://github.com/simplilearn-github/Pipeline_Script.git'
			}
		}
		
		stage('Build') {
			steps{
				bat 'Build.bat'
			}
		}
		
		stage('Testing'){
			parallel{
				stage('Unit-Testing') {
					agent{
						label 'Windows_Slave'
					}
					steps{
						echo "Unit-Testing executing in Windows_Slave"
						git 'https://github.com/simplilearn-github/Pipeline_Script.git'
						bat 'Unit.bat'
					}
				}
				stage('Quality-Test') {
					agent{
						label 'master'
					}
					steps{
						echo "Quality-Testing executing in master"
						git 'https://github.com/simplilearn-github/Pipeline_Script.git'
						bat 'Quality.bat'
					}
				}
			}
		}
		
		stage('Deploy') {
			steps{
				bat 'Deploy.bat'
			}
		}
    }
}
