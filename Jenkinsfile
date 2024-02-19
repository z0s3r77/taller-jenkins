pipeline{

	agent any
	stages {
	stage('Obtener el repositorio') {
		steps {
			git branch: 'master', url: 'https://github.com/z0s3r77/taller-jenkins'
		}

	}

	stage('Construir la documetación') {
            steps {
                sh "doxygen"
            }    
        }

	stage('Archivar la documentación') {
            steps {
                sh "zip documentation.zip -r html/*"
            }
        }


        stage('Análisis estático') {
            steps {
                sh 'make cppcheck-xml'
                recordIssues enabledForFailure: true, failOnError: true, qualityGates: [[threshold: 1, type: 'TOTAL', unstable: false]], tools: [cppCheck(pattern: 'reports/cppcheck/*.xml')]
            }
        }



	
	}



	   post {
        success {
            publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'html/', reportFiles: 'files.html', reportName: 'Documentación', reportTitles: ''])
            archive "documentation.zip"
        }
    }

}
