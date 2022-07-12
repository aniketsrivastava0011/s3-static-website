pipeline {

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git branch: "main",
          // credentialsId: '',
          url: 'https://github.com/aniketsrivastava0011/s3-static-website.git'
      }
    }

    stage('Upload to S3') {
        steps{
            script {

                dir(){

                    pwd(); //Log current directory

                    withAWS(region:'ap-south-1',credentials:'s3-static-website') {

                        def identity=awsIdentity();//Log AWS credentials

                        // Upload files from working directory '' in your project workspace
                        s3Upload(bucket:"s3-static-website", workingDir:'', includePathPattern:'**/*');
                        // invalidate CloudFront distribution
                       // cfInvalidate(distribution:'E152QNNVYS423', paths:['/*'])
                    }

                };
            }
        }
    }

  }

}
