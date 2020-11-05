# Configure Keptn

In this lab you'll configure keptn to expand the quality gates capabilities and use it for continuous delivery.

## Step 1: Configure Keptn for continuous delivery

1. Reinstall keptn with the continuous delivery capabilities enabled and to change how we expose keptn:

   ```bash
    (bastion)$ keptn uninstall
    (bastion)$ keptn install --endpoint-service-type=ClusterIP --use-case=continuous-delivery
    ```

---

[Previous Step: Preparation](../00_Preparation):arrow_backward: :arrow_forward: [Next Step: Configure Istio](../02_Configure Istio)

:arrow_up_small: [Back to overview](../)
