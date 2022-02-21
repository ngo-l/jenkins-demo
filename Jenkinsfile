def label = "worker-${UUID.randomUUID().toString()}"

podTemplate(label: label, containers: [
  containerTemplate(name: 'buildsh', image: 'ngol/dev3:v1', command: 'cat', ttyEnabled: true),
  containerTemplate(name: 'kubectl', image: 'lachlanevenson/k8s-kubectl:v1.8.8', command: 'cat', ttyEnabled: true),
  containerTemplate(name: 'helm', image: 'lachlanevenson/k8s-helm:latest', command: 'cat', ttyEnabled: true)
],
volumes: [
  hostPathVolume(mountPath: '/mnt', hostPath: '/mnt')
]) {
  node(label) {
//     def myRepo = checkout scm
//     def gitCommit = myRepo.GIT_COMMIT
//     def gitBranch = myRepo.GIT_BRANCH
//     def shortGitCommit = "${gitCommit[0..10]}"
//     def previousGitCommit = sh(script: "git rev-parse ${gitCommit}~", returnStdout: true)
//
//     stage('Test') {
//       try {
//         container('buildsh') {
//           sh """
//             pwd
//             echo "GIT_BRANCH=${gitBranch}" >> /etc/environment
//             echo "GIT_COMMIT=${gitCommit}" >> /etc/environment
//             cat /etc/*release*
//             """
//         }
//       }
//       catch (exc) {
//         println "Failed to test - ${currentBuild.fullDisplayName}"
//         throw(exc)
//       }
//     }
    stage('Build') {
      container('buildsh') {
        echo "test"
        sh "ls /mnt"
        sh "df -h"
        sh "touch /mnt/test.txt"
      }
    }

    stage('Run kubectl') {
      container('kubectl') {
        sh "kubectl version"
        sh "ls /mnt"
      }
    }
    stage('Run helm') {
      container('helm') {
        sh "helm version"
        sh "ls /mnt"
      }
    }
  }
}
