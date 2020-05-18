pipeline {
  agent any
       stages {
          stage('Build') {
            // Build an image for scanning
            sh 'echo "FROM imiell/bad-dockerfile:latest" > Dockerfile'
            sh 'docker build --no-cache -t test/test-image:0.1 .'
          }

          stage('Scan') {
            // Scan the image
            prismaCloudScanImage ca: '',
            cert: '',
            dockerAddress: 'unix:///var/run/docker.sock',
            image: 'test/test-image*',
            key: '',
            logLevel: 'info',
            podmanPath: '',
            project: '',
            resultsFile: 'prisma-cloud-scan-results.json',
            ignoreImageBuildTime:true
          }
       }

       post { // The post section lets you run the publish step regardless of the scan results
            always {
                prismaCloudPublish resultsFilePattern: 'prisma-cloud-scan-results.json'
            }
       }
}