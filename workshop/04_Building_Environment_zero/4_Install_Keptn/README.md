# Install keptn
We will install [Keptn](https://keptn.sh/) on your GKE cluster and use the quality gates and self-healing capabilities in the following labs.

## Step 1: Verify the keptn CLI has already been installed
1. Execute the following command to check the keptn CLI has been installed
    ```
    (bastion)$ keptn
    ```
1. You will be presented with a response like the following:
![keptn](../assets/keptnCLI.png)


# Step 2: Install the keptn runtime
1. To install the keptn runtime on your cluster, execute the following command:
    ```
    (bastion)$ keptn install --endpoint-service-type=LoadBalancer --use-case=continuous-delivery
    ```
2. The installer will ask you for the following information:
    - Cluster name (should already be prefilled)

![keptn](./assets/keptn-Install.png)

1. Confirm your entry. The keptn installation process will commence.

![keptn_install](./assets/keptn_installation_logs.png)