pipeline {
    agent any
    environment {
        GO111MODULE = 'auto'
        // This can be nexus3 or nexus2
        NEXUS_VERSION = "nexus3"
        // This can be http or https
        NEXUS_PROTOCOL = "http"
        // Where your Nexus is running
        NEXUS_URL = "192.168.100.14:18081"
        // Repository where we will upload the artifact
        //NEXUS_REPOSITORY = "golang"
        NEXUS_REPOSITORY = "nuget-hosted"
        // Jenkins credential id to authenticate to Nexus OSS
        NEXUS_CREDENTIAL_ID = "admin"
        ARTIFACT_NAME = "helloprogramm.run"
        ARTIFACT = "helloprogramm"
    }
    stages {
        //stage("clone code") {
        //    steps {
        //        script {
                    // Let's clone the source
         //           git 'https://github.com/anrystate86/goHello.git';
         //       }
        //  }
        //}
        stage('build') {
            steps {
                 //sh 'ls -ahl'
                 //sh 'pwd'
                 sh 'go build -o $ARTIFACT_NAME' //helloprogramm.run
                 //sh 'ls -ahl'
            }
        }
        stage("publish to nexus") {
            steps {
                script {
                    artifactPath = ARTIFACT_NAME;
                    // Assign to a boolean response verifying If the artifact name exists
                    artifactExists = fileExists artifactPath;
                    if(artifactExists) {
                        //echo "*** File: ${artifactPath}, group: ${pom.groupId}, packaging: ${pom.packaging}, version ${pom.version}";
                        echo "*** File: ${artifactPath}";
                        nexusArtifactUploader {
                          nexusVersion('nexus3')
                          protocol('http')
                          nexusUrl('192.168.100.14:18081')
                          groupId('test')
                          version('1')
                          repository('nuget-hosted')
                          credentialsId('admin')
                          artifact {
                            artifactId('helloprogramm')
                            type('run')
                            classifier('debug')
                            file('helloprogramm.run')
                          }
                        //artifact {
                        //    artifactId('nexus-artifact-uploader')
                        //    type('hpi')
                        //    classifier('debug')
                        //    file('nexus-artifact-uploader.hpi')
                        //}
                      }
//                        nexusArtifactUploader(
//                            nexusVersion: NEXUS_VERSION,
//                            protocol: NEXUS_PROTOCOL,
//                            nexusUrl: NEXUS_URL,
//                            groupId: 'group',
//                            version: '1',
//                            repository: NEXUS_REPOSITORY,
//                            credentialsId: NEXUS_CREDENTIAL_ID,
//                            artifacts:  [
//                                [artifactId: ARTIFACT,
//                                classifier: '1',
//                                file: ARTIFACT_NAME,
//                                type: 'run'],
//                            ]
//                        );

                    } else {
                        error "*** File: ${artifactPath}, could not be found";
                    }
                }
            }
        }
    }

}
