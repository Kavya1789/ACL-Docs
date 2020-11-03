# Run Performance Test on Carts Service

In this lab you'll measure the performance for the carts service 3 times. The first time you'll run the test and create a baseline for future runs. The second time you will introduce a small delay that will be evaluated as a warning SLO result. The third time you will increase the delay to see how the pipelines fails when breaking the SLO rule.

## Step 1: Run Performance Test on current Implementation

1. Go to  **Jenkins** and click on **sockshop** folder.
1. Click on **carts.performance**.
1. Click on **Build with parameters** to trigger the performance pipeline. (leave the default values).
1. Wait until the pipeline shows: *Success*.

## Step 2: Introduce a slowdown in the Carts Service

1. In the directory of `carts\`, open the file: `carts\src\main\resources\application.properties`.
1. Change the value of `delayInMillis` from `0` to `200`.
1. Commit/Push the changes to your GitHub Repository *carts*.

## Step 3: Build this new Version

1. Go to **Jenkins** and click on the **sockshop** folder.
1. Click on **carts** and select the **master** branch.
2. Click on **Build Now** to trigger the pipeline. 
3. Wait until the pipeline shows: *Success*.

## Step 4: Run Performance Test on new Version

1. Go to **Jenkins** and click on the **sockshop** folder.
1. Click on **carts.performance** and select the **master** branch.  
1. Click on **Build with parameters** to trigger the performance pipeline (leave the default values).
2. Wait until the pipeline shows: *Warning* (yellow color).


## Step 5: Explore Results in Keptn bridge

1. After the pipeline finished the job click on the job ID and then go to Console Output to visualize the pipeline results.


## Step 6: Explore Results in Dynatrace


---

[Previous Step: Define Performance Pipeline](../04_Define_Performance_Pipeline) :arrow_backward: :arrow_forward: [Next Step: Compare Tests in Dynatrace](../06_Compare_Tests_in_Dynatrace)

:arrow_up_small: [Back to overview](../)
