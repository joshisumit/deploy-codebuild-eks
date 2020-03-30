Deploy to EKS cluster from CodeBuild
1. In the buildspec.yaml, change the [kubectl binary version](https://github.com/joshisumit/deploy-codebuild-eks/blob/9bf2238ad2697a826a8d0fbc30090d1a08b5891d/buildspec.yml#L6) and [EKS cluster region and Cluster name](https://github.com/joshisumit/deploy-codebuild-eks/blob/9bf2238ad2697a826a8d0fbc30090d1a08b5891d/buildspec.yml#L11) to match with your EKS cluster (currently it uses EKS v1.15)

2. Allow CodeBuild Service IAM role in [aws-auth ConfigMap](https://docs.aws.amazon.com/eks/latest/userguide/add-user-role.html)
   - kubectl -n kube-system edit cm aws-auth
   - Add CodeBuild service IAM role under mapRoles section:
  
```
mapRoles: |
    - groups:
      - system:masters
      rolearn: arn:aws:iam:123456789012:role/KubernetesRole  #<---- codebuild is assuming this IAM role
      username: KubernetesRole
```

3. Create a CodeBuild project with following configs to deploy the pod/application on every push/pull request
- [Github source provider](https://docs.aws.amazon.com/codebuild/latest/userguide/sample-source-version.html) 
- [Webhook](https://docs.aws.amazon.com/codebuild/latest/userguide/sample-github-pull-request.html)\
- Add 3 env-variables: ECR_REPO_URI, EKS_CLUSTER_NAME, EKS_VERSION
