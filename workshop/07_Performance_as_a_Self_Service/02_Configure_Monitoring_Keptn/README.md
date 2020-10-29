# Configure monitoring with Dynatace
In order to use Keptn with Dynatrace we will need to install the Dynatrace service and Dynatrace SLI service.

## Step 1: Configure the Dynatrace Service for keptn

The OneAgent Operator has already been deployed in earlier stages of the lab. However, we still need to install the Dynatrace Service for keptn which will allow keptn to communicate with Dynatrace for sending events and comments to Problems.

1. Execute the following command from your home directory to install the Dynatrace Service for keptn

    ```bash
    (bastion)$ cd
    (bastion)$ ./installDynatraceServiceForKeptn.sh
    ```

1. This script will perform the following steps:
    - Configure automated tagging rules in Dynatrace for environment, service and test-subject
    - Configure a problem notification in Dynatrace for sending events to the keptn api
    - Set up the Dynatrace Service in keptn



## Step 2: Install Dynatrace SLI service
In order to allow Keptn to use Dynatrace as an SLI provider we will need to install the [Dynatrace SLI Service](https://github.com/keptn-contrib/dynatrace-sli-service) for Keptn.

    (bastion)$ kubectl apply -f https://raw.githubusercontent.com/keptn-contrib/dynatrace-sli-service/0.7.0/deploy/service.yaml 

You should get as a response the following message

    serviceaccount/keptn-dynatrace-sli-service created
    role.rbac.authorization.k8s.io/keptn-dynatrace-sli-service-secrets created
    rolebinding.rbac.authorization.k8s.io/keptn-dynatrace-sli-service-secrets created
    deployment.apps/dynatrace-sli-service created
    service/dynatrace-sli-service created
