import jenkins.model.*
import hudson.model.*
import java.time.*

def JenkinsNodes=["AzureAgent06", "AzureAgent01", "AzureAgent02", "AzureAgent03", "AzureAgent04", "AzureAgent05"]

def Clean(NodeName) {
    script{
           sh """
           echo ${NodeName} 
            """
            }
        }

pipeline {

    agent {
        node {
            label 'master'||'AzureAgent06||AzureAgent01||AzureAgent02||AzureAgent03||AzureAgent04||AzureAgent05'
        }
    }

    stages {
        stage ('Clean Containers') {
            steps {
                script {
                    $JenkinsNodes.each {
                        println("Node $it")
                    }
                }
            }
        }
                stage ('Clean Images') {
            steps {
                script {
                    $JenkinsNodes.each {
                        println("Node $it")
                    }
                }
            }
        }
    }
}
