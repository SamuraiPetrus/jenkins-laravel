def ConnectSSHAndExecuteCommands(host, user, credentialId, commands) {
  sshagent(credentials : ["${credentialId}"]) {
    sh "ssh -t -t ${user}@${host} -o StrictHostKeyChecking=no '${commands.join(' && ')}'"
  }
}

pipeline {
    agent any
    stages {
        stage("Build") {
            steps {
                sshPublisher(publishers: [sshPublisherDesc(configName: 'Laravel Client', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '**/**')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
                
                ConnectSSHAndExecuteCommands('34.237.238.206', 'ubuntu', 'jenkins-laravel',
                    [
                        'php --version',
                    ]
                )
            }
        }
    }
}