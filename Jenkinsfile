pipeline {
	agent any

	options {
		buildDiscarder(logRotator(numToKeepStr: '2', artifactNumToKeepStr: '1'))
		timestamps()
    	timeout(time: 5, unit: 'MINUTES')
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
