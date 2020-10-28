import jenkins.model.*
import hudson.model.*
import java.time.*

def Clean(NodeName) {
    script{
           sh """
            echo "Stopped containers:"
            for container in `docker ps -a | grep -v CONTAINER | grep -v UP | awk '{print $1}'`; do echo $container; done;
            echo "Images:"
            for image in `docker image ls | grep -v REPOSITORY | awk '{print $3}'`; do echo $image; done;
            echo "Done"
            """
            }
        }

pipeline {
    triggers {
        cron('''TZ=Europe/Kiev
        20 15 * * *''')
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
                      def JenkinsNodes = 'AzureAgent06, AzureAgent01, AzureAgent02, AzureAgent03, AzureAgent04, AzureAgent05'
                      JenkinsNodes.tokenize(',').each {
                        stage("${it}") {
                            node { label "${it}"}
                            script{
                                Clean("${it}")
                            }
                        }
                      }
                    }
                }
            }
        }
    }
}
