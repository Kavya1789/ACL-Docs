# Configure Keptn

In this lab you'll configure Keptn to expand the capabilities and use it for continuous delivery.

## Step 1: Configure Keptn for continuous delivery 

1. We will need to reinstall keptn with the continuous delivery as the use case.
   ```bash
    (bastion)$ keptn install --endpoint-service-type=LoadBalancer --use-case=continuous-delivery
    ```
