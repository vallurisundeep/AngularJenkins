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

                    dir(deploymentDir) {
                        // Clean up existing deployment files if they exist
                        bat "del /F /Q *"

                        // Copy files to deployment directory
                        bat "xcopy /S /Y ..\\dist\\* ."
                    }

                    // Copy deployment files to htdocs
                    bat "xcopy /S /Y ${deploymentDir}\\* ${htdocsPath}"
                }
            }
        }
    }
}
