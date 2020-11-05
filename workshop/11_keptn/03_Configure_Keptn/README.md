# Configure keptn

Since we have chnged the way keptn is exposed from using a LoadBalancer service to istio, the keptn CLI will need to be reauthenticated.

## Step 1: Authenticate keptn CLI

1. Export the keptn api endpoint and API token as environment variables

    ```bash
    (bastion)$ export KEPTN_ENDPOINT=http://$(kubectl -n keptn get ingress api-keptn-ingress -ojsonpath='{.spec.rules[0].host}')/api
    (bastion)$ export KEPTN_API_TOKEN=$(kubectl get secret keptn-api-token -n keptn -ojsonpath='{.data.keptn-api-token}' | base64 --decode)
    ```

1. Use this stored information and authenticate the CLI.

    ```bash
    (bastion)$ keptn auth --endpoint=$KEPTN_ENDPOINT --api-token=$KEPTN_API_TOKEN
    ```

## Step 2: Authenticate keptn bridge

After installing and exposing Keptn, you can access the Keptn Bridge by using a browser and navigating to the Keptn endpoint.

1. To get the keptn bridge url, run the following commmands:

    ```bash
    (bastion)$ export KEPTN)_BRIDGE=http://$(kubectl -n keptn get ingress api-keptn-ingress -ojsonpath='{.spec.rules[0].host}')/bridge
    ```

1. The keptn bridge has basic authentication enabled by default and the default user is keptn with an automatically generated password.

    ```bash
    (bastion)$ keptn configure bridge --output
    ```

## Step 3: Configure the Dynatrace Service for Keptn

1. Execute the following command from your home directory to install the Dynatrace Service for Keptn

    ```bash
    (bastion)$ cd
    (bastion)$ ./installDynatraceServiceForKeptn.sh
    ```

[Previous Step: Configure istio](../02_Configure_Istio):arrow_backward::arrow_forward: [Next Step: Onboard Service](../04_Onboard_Service)

:arrow_up_small: [Back to overview](../)