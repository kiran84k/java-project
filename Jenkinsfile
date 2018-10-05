pipeline {
	agent {
		label 'slave' 
	}

	stages{
		stage('Junit test'){
			steps{
				sh 'ant -f test.xml -v'
				junit 'reports/result.xml'
			}
		}
		stage('build'){
			steps{
				sh 'ant -f build.xml -v'
			}
		}

	}

	post {
		always {
			archiveArtifacts 'dist/*.jar'
		}
	}
}
