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

                    // Delete existing deployment directory if it exists
                    if (isDirectoryExists(deploymentDir)) {
                        bat "rd /s /q ${deploymentDir}"
                    }

                    // Create deployment directory
                    bat "mkdir ${deploymentDir}"

                    // Copy files to deployment directory
                    bat "xcopy /S /Y dist\\* ${deploymentDir}\\"

                    // Copy deployment files to htdocs
                    bat "xcopy /S /Y ${deploymentDir}\\* ${htdocsPath}"
                }
            }
        }
    }
}

def isDirectoryExists(directoryPath) {
    return bat(script: "if exist \"${directoryPath}\" echo true", returnStdout: true).trim() == "true"
}
