![Build Status](https://codebuild.eu-west-1.amazonaws.com/badges?uuid=eyJlbmNyeXB0ZWREYXRhIjoiL29xUld2UTFRNUp1Zi9UUTZUUmVWTVMxV0N0Szk4WTVIeHh3dEFLMHJKbCs2TFE2S3JDZ1U0eFZ4Um84TStncWVNS0FFMWVqVWl2VEdrVDE4bms2TVNRPSIsIml2UGFyYW1ldGVyU3BlYyI6IjhmeUR5M1d4Yk9CVzdIOHYiLCJtYXRlcmlhbFNldFNlcmlhbCI6MX0%3D&branch=master)


Deploy to EKS cluster from CodeBuild
1. In the buildspec.yaml, change the [kubectl binary version](https://github.com/joshisumit/deploy-codebuild-eks/blob/9bf2238ad2697a826a8d0fbc30090d1a08b5891d/buildspec.yml#L6) and [EKS cluster region and Cluster name](https://github.com/joshisumit/deploy-codebuild-eks/blob/9bf2238ad2697a826a8d0fbc30090d1a08b5891d/buildspec.yml#L11) to match with your EKS cluster (currently it uses EKS v1.14)
2. Allow CodeBuild Service IAM role in [aws-auth ConfigMap](https://docs.aws.amazon.com/eks/latest/userguide/add-user-role.html)
3. Create a CodeBuild project with [Github source provider](https://docs.aws.amazon.com/codebuild/latest/userguide/sample-source-version.html) and [Webhook](https://docs.aws.amazon.com/codebuild/latest/userguide/sample-github-pull-request.html) to deploy the pod/application on every push/pull request

