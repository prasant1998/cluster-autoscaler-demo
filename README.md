# Cluster Autoscaler (CA)

## In eks-nodes-role, need to add an extra policy with below permissions -
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "autoscaling:DescribeAutoScalingGroups",
                "autoscaling:DescribeAutoScalingInstances",
                "autoscaling:DescribeLaunchConfigurations",
                "autoscaling:DescribeTags",
                "autoscaling:SetDesiredCapacity",
                "autoscaling:TerminateInstanceInAutoScalingGroup",
                "ec2:DescribeLaunchTemplateVersions"
            ],
            "Resource": "*"
        }
    ]
}
```

## Need to specify your cluster name -
```
--node-group-auto-discovery=asg:tag=k8s.io/cluster-autoscaler/enabled,k8s.io/cluster-autoscaler/<YOUR CLUSTER NAME>
```

## Find the sutable version of cluster autoscaller image according to your EKS cluster and replace the following line - 
The CA version is also similar like your EKS version i.g. - v1.30.n
```
registry.k8s.io/autoscaling/cluster-autoscaler:v1.30.1
```
#### from here you can find the release list of versions - https://github.com/kubernetes/autoscaler/releases

## To view the log that the CA is working fine -
```
kubectl -n kube-system logs -f deployment.apps/cluster-autoscaler
```
If it shows any error then your setup is wrong

## Demo app to test the Cluster Autoscaller -
```
kubectl apply -f app-deploy.yml
```