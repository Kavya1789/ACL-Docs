# Analyze results in Keptn Bridge

In this lab you'll learn how to leverage Keptn bridge to analyze the differences between the three performance tests and it's relation to the SLO definitions.

![keptn-bridge](./assets/keptn-bridge.png)
## Step 1: Go to the keptn bridge
1. Go to the Keptn bridge url and use the url, username and password from [Install keptn lab](../01_Install_Keptn).

2. Select the project you want to visualize using the top dropdown.

3. Click on the carts service and select the Evaluation started event.

As you can see, the right panel shows the history for the deployment event and the evaluation result compare with the previous builds for each SLO defined.

During our first run the 2 SLO objectives were fulling with   values:
```
- response_time_p95: 258ms (this can be a different value during your run, we will see why by using Dynatrace during the next lab)
- error_rate: 0%
```

During our second run, the 1 of the 2 SLO hit the warning zone set between 400ms to 700ms for response_time_p95.
```
- response_time_p95: 636ms (this can be a different value during your run, we will see why by using Dynatrace during the next lab)
- error_rate: 0%
```
During our third run, the 1 of the 2 SLO hit the failure zone getting a result over 700ms response_time_p95.
```
- response_time_p95: 885ms (this can be a different value during your run, we will see why by using Dynatrace during the next lab)
- error_rate: 0%
```

---

[Previous Step: Run Performance Tests](../07_Run_Performance_Tests) :arrow_backward: :arrow_forward: [Next Step: Compare Test in Dynatrace](../09_Compare_Test_in_Dynatrace)

:arrow_up_small: [Back to overview](../)