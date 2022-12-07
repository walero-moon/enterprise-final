// Name: Victor Leopoldino Sanches Valero
// Student ID: A01210162
// Description: This Jenkinsfile installs the required python dependencies and
// and checks for code quality and quantity. It then runs the scripts and Zips
// all files in the project.

pipeline {
    agent any
    parameters {
        string(name: 'TARGET', defaultValue: '', description: 'Run Target Scripts')
    }
    stages {
        stage('Build') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }
        stage('Code Quality') {
            steps {
                sh 'pylint-fail-under --fail_under 7.0 *.py'
            }
        }
        stage('Code Quantity') {
            steps {
                sh 'for i in *.py; do wc -l $i; done'
            }
        }
        stage('Run Scripts') {
            when {
                expression { params.TARGET == 'run' }
            }

            steps {
                sh 'python3 main.py phone text output'
                sh 'python3 main.py tablet csv output'
                sh 'python3 main.py laptop json output'
            }
        }
        stage('Zip') {
            steps {
                sh 'zip -r app.zip *.py'
                archiveArtifacts artifacts: 'app.zip'
            }
        }
    }
}