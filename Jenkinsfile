pipeline {
	agent any

	options {
		buildDiscarder(logRotator(NumToKeep: '2', artifactNumToKeep: '1'))
	}


	stages {
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
