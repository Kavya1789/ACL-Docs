# Configure Keptn

In this lab you'll configure keptn to expand the quality gates capabilities and use it for continuous delivery.

## Step 1: Configure Keptn for continuous delivery

1. Redeploy keptn with the continuous delivery capabilities enabled

   ```bash
    (bastion)$ keptn install --endpoint-service-type=ClusterIP --use-case=continuous-delivery
    ```

---
[Previous Step: Configure Istio](../01_Configure_Istio):arrow_backward: :arrow_forward: [Next Step: Onboard service](../03_Onboard_Service)

:arrow_up_small: [Back to overview](../)
