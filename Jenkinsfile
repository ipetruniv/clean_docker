import jenkins.model.*
import hudson.model.*
import java.time.*

pipeline {
    triggers {
        cron('''TZ=Europe/Kiev
        20 15 * * *''')
    }

    agent {
        node {
            label 'AzureAgent'
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
                                sh"""#!/bin/bash
                                    echo "Stopped containers:"
                                    docker ps -a
                                    echo "Images:"
                                    docker images ls
                                    echo "Done"
                                    """
                            }
                        }
                    }
                }
            }
        }
    }
}

