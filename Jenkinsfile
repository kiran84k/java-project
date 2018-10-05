pipeline {
	agent any

	options {
		buildDiscarder(logRotator(NumToKeepStr: '2', artifactNumToKeepStr: '1'))
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
