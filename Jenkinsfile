@Library('jenkins_libraries') _

pipeline {
    agent any
    stages {
            stage('Checkout') {
                steps{
                    checkout scm
                }
            }
            stage('Running terraform format'){
                steps{
                    script {
                        terraformTest.tffmt()
                    }
                }
            }
            stage('Running terraform init'){
                steps {
                    script{
                        terraformTest.tfinit()
                    }
                }
            }
            stage('Running terraform validate'){
                steps {
                    script{
                        terraformTest.tfvalidate()
                    }
                }
            }
            stage('Running terraform plan'){
                steps {
                    script {
                        terraformTest.tfplan()
                    }
                }
            }
            stage('Validate pipeline results'){
                steps {
                    input "Approve Deploy?"
                }
            }
            stage('Deploy') {
                steps {
                    script{
                        deployTerraform.tfapply()
                    }
                }
            }
            stage('destroy'){
                steps {
                    script{
                        deployTerraform.tfdestroy()
                    }
                }
            }
        }
}
