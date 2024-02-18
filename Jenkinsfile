pipeline{

	agent any
	stages {
	stage('Obtener el repositorio') {
		steps {
			git branch: 'main', url: 'https://github.com/z0s3r77/taller-openwebinars'
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
	
	}

	   post {
        success {
            publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'html/', reportFiles: 'files.html', reportName: 'Documentación', reportTitles: ''])
            archive "documentation.zip"
        }
    }

}
