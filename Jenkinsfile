import jenkins.model.*
import hudson.model.*
import java.time.*

def Clean(NodeName) {
    script{
           sh """
           echo ${NodeName} 
            """
            }
        }

pipeline {
    parameters {
        string(name: "JenkinsNodes",
        defaultValue: "AzureAgent06, AzureAgent01, AzureAgent02, AzureAgent03, AzureAgent04, AzureAgent05",
        description: "Comma separated Jenkins nodes to clean docker")
    }

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
                      NodesList = "${JenkinsNodes}".split(', ')
                      println("${NodesList}")

                      NodeListLenght = NodesList.length - 1
                      println("${NodeListLenght}")

                      for ( idx=0; idx<NodeListLenght; idx+=1 ){
                        def NodeName=NodeList[idx]
                        Clean(NodeName)
                        }
                    }
                }
            }
        }

        stage ('Clean Images') {
            steps {
                script {
                     catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') { 
                     NodesList.eachWithIndex  {
                        println("Index: $i Value: $it")
                    }
                    }
                }
            }
        }
    }
}
