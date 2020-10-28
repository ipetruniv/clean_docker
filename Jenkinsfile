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
                                sh("""#!/bin/bash
                                    echo "Stopped containers:"
                                    docker ps -a
                                    for container in \$(docker ps -a | grep -v CONTAINER | grep -v UP | awk \'{print \$1}\'); do echo \$container; done;
                                    echo "Images:"
                                    for image in `docker image ls | grep -v REPOSITORY | awk \'{print \$3}\'`; do echo \$image; done;
                                    docker images ls
                                    echo "Done"
                                    """)
                            }
                        }
                    }
                }
            }
        }
    }
}

