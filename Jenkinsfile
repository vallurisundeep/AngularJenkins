pipeline {
    agent any

    stages {
        stage("Print Node version") {
            steps {
                bat 'node -v'
            }
        }

        stage("Git clone Angular project") {
            steps {
                git branch: 'main', url: 'https://github.com/vallurisundeep/AngularJenkins'
            }
        }

        stage("npm install") {
            steps {
                bat 'npm install'
            }
        }

        stage("ng build") {
            steps {
                bat 'ng build --configuration=production --base-href ./'
            }
        }

        stage("Deployment") {
            steps {
                script {
                    def deploymentDir = "deployment"
                    def htdocsPath = "C:\\xampp\\htdocs"

                    if (!fileExists(deploymentDir)) {
                        bat 'mkdir deployment'
                    }

                    bat "xcopy /S /Y dist\\* ${deploymentDir}\\"

                    bat "xcopy /S /Y ${deploymentDir}\\* ${htdocsPath}"
                }
            }
        }
    }
}

def fileExists(filePath) {
    return new File(filePath).exists()
}
