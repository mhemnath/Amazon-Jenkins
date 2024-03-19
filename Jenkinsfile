pipeline {
    agent any
    
    stages {
        stage('Checkout Feature Branch') {
            steps {
                // Checkout source code from the feature branch
                git branch: 'devops', url: 'https://github.com/mhemnath/Amazon-Jenkins.git'
            }
        }
        stage('Build and Test') {
            steps {
                // Build and run tests on the feature branch
                sh 'mvn clean test' // Replace with your build and test commands
            }
        }
        stage('Merge into Main') {
            when {
                // Condition to check if the previous stage was successful
                expression { currentBuild.previousBuild?.result == 'SUCCESS' }
            }
            steps {
                // Merge changes into the main branch
                script {
                    // Checkout main branch
                    sh 'git checkout main'
                    // Merge feature branch into main
                    sh 'git merge devops'
                    // Push changes to the remote repository
                    sh 'git push origin main'
                }
            }
        }
    }
}
