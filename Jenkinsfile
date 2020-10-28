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
            label 'AzureAgent06||AzureAgent01||AzureAgent02||AzureAgent03||AzureAgent04||AzureAgent05'
            customWorkspace "workspace/cps_angular_test_$BRANCH_NAME"
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
