pipeline {
	agent none

	options {
		buildDiscarder(logRotator(numToKeepStr: '2', artifactNumToKeepStr: '1'))
		timestamps()
    	timeout(time: 5, unit: 'MINUTES')
	}

	stages{
		stage('Junit test'){
      agent{ 
        label 'apache'
        }
			steps{
				sh 'ant -f test.xml -v'
				junit 'reports/result.xml'
			}
		}
		stage('build'){
			agent{ 
        label 'apache'
        }
      steps{
				sh 'ant -f build.xml -v'
			}
		}
		stage('deploy'){
			agent{ 
        label 'apache'
        }
      steps{
				sh "cp dist/rectangle_${env.BUILD_NUMBER}.jar /var/www/html/rectangles/all"
			}
		}
    stage('running on master'){
      agent {
        label 'master'
      }
      steps{
        sh "/usr/local/bin/wget http://192.168.56.120/rectangles/all/rectangle_${env.BUILD_NUMBER}.jar"
        sh "java -jar rectangle_${env.BUILD_NUMBER}.jar 3 4"

      }
    }
	}

	post {
		always {
			archiveArtifacts 'dist/rectangle_${env.BUILD_NUMBER}.jar'
		}
	}
}
