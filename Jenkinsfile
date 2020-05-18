pipeline {
  agent any
       stages {
          stage('Build') {
            // Build an image for scanning
            steps {
                echo "DO NOTHING"
                // sh 'echo "FROM imiell/bad-dockerfile:latest" > Dockerfile'
                // sh 'docker build --no-cache -t test/test-image:0.1 .'
            }
          }

          stage('Scan') {
            // Scan the image
            steps {
                // sh '/bin/twistcli images scan nginx:latest --docker-address unix:///var/run/docker.sock --min-scan-time 1589822113682 --ci --publish --details --address https://us-east1.cloud.twistlock.com/us-1-111574323 --ci-results-file prisma-cloud-scan-results.json --http-proxy admin:804965f4d71c4f968d1f4c564aa27f81@webcache.comp.pge.com:8080'
                prismaCloudScanImage ca: '',
                cert: '',
                dockerAddress: 'unix:///var/run/docker.sock',
                image: 'nginx:latest',
                key: '',
                logLevel: 'info',
                podmanPath: '',
                project: '',
                resultsFile: 'prisma-cloud-scan-results.json',
                ignoreImageBuildTime:true
            }
          }
       }

       post { // The post section lets you run the publish step regardless of the scan results
            always {
                prismaCloudPublish resultsFilePattern: 'prisma-cloud-scan-results.json'
            }
       }
}