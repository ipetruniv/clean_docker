import jenkins.model.*
import hudson.model.*
import java.time.*

def JenkinsNodes = ["AzureAgent06", "AzureAgent01", "AzureAgent02", "AzureAgent03", "AzureAgent04", "AzureAgent05"]

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
            label 'dev'
        }
    }

    stages {
        stage ('Clean Containers') {
            steps {
                script {
                     catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                        Clean("Stage")
                     }
                    }
                }
            }

        stage ('Clean Images') {
            steps {
                script {
                     catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    $JenkinsNodes.eachWithIndex  {
                        println("Index: $i Value: $it")
                    }
                    }
                }
            }
        }
    }
}
