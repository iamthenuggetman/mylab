pipeline {
    //Directives
    agent any
    tools {
        maven 'maven'
    }
    environment {
        ArtifactId = readMavenPom().getArtifactId()
        Version = readMavenPom().getVersion()
        Name = readMavenPom().getName()
        GroupID = readMavenPom().getGroupId()
    }

    stages {
        // Specify various stage with in stages

        // stage 1. Build
        stage('Build') {
            steps {
                sh 'mvn clean install package'
            }
        }

        // Stage2 : Testing
        stage('Test') {
            steps {
                echo ' testing......'

            }
        }

        // Stage3 : Publish the artifacts to Nexus
        stage('Publish to Nexus') {
            steps {
                script {
                    def NexusRepo = Version.endsWith("SNAPSHOT") ? "VinaysDevOpsLab-SNAPSHOT" : "VinaysDevOpsLab-RELEASE"

                    nexusArtifactUploader artifacts: [
                            [
                                artifactId: "${ArtifactId}",
                                classifier: '',
                                file: "target/${ArtifactId}-${Version}.war",
                                type: 'war'
                            ]
                        ],
                        credentialsId: '54b85066-304b-40b5-a8af-fc52c2c323ce',
                        groupId: "${GroupId}",
                        nexusUrl: '172.20.10.24:8081',
                        nexusVersion: 'nexus3',
                        protocol: 'http',
                        repository: "${NexusRepo}",
                        version: "${Version}"
                }
            }
        }

        stage('Print environment variables') {
            steps {
                echo "ArtificatID is '${ArtifactId}'"
                echo "Version is '${Version}'"
                echo "GroupID is '${GroupId}'"
                echo "Name is '${Name}'"
            }
        }

        // Stage5 : Deploying
        // stage ('Deploying'){
        //     steps {
        //         echo ' Deploying......'

        //     }
        // }

    }

}