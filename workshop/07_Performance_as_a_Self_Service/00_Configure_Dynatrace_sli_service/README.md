# Install Dynatrace SLI service
In order to allow Keptn to use Dynatrace as an SLI provider we will need to install the [Dynatrace SLI Service](https://github.com/keptn-contrib/dynatrace-sli-service) for Keptn.

    (bastion)$ kubectl apply -f https://raw.githubusercontent.com/keptn-contrib/dynatrace-sli-service/0.7.0/deploy/service.yaml 

You should get as a response the following message

    serviceaccount/keptn-dynatrace-sli-service created
    role.rbac.authorization.k8s.io/keptn-dynatrace-sli-service-secrets created
    rolebinding.rbac.authorization.k8s.io/keptn-dynatrace-sli-service-secrets created
    deployment.apps/dynatrace-sli-service created
    service/dynatrace-sli-service created
