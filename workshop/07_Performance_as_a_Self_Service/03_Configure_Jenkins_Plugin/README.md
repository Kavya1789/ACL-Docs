# Configure Keptn library for Jenkins
In this lab you'll learn how to configure the Keptn library for Jenkins.
![keptn](./assets/evalpipeline_animated.gif)

## Step 1: Review keptn library installation
Go into Jenkins and review the keptn library installation `Jenkins > Manage Jenkins > Configure System >Global Pipeline Libraries`.
![keptn](./assets/keptn-jenkins-library.PNG)

## Step 2: Review and uncomment the Jenkinsfile 

Review the pipeline definition file located in the repository `carts/JenkinsFile`. 
![keptn](./assets/keptn-jenkinspipeline0.PNG)
![keptn](./assets/keptn-jenkinspipeline1.PNG)

To activate the pipeline you will have to first uncomment the following part from the file located in `k8s-deploy-to-staging/JenkinsFile`
````
...
// DO NOT uncomment until 7_03 Lab
    stage('Keptn Init') {
      steps{
        script {
          keptn.keptnInit project:"${KEPTN_PROJECT}", service:"${KEPTN_SERVICE}", stage:"${KEPTN_STAGE}", monitoring:"${KEPTN_MONITORING}", shipyard: "${KEPTN_SHIPYARD}"
          keptn.keptnAddResources("${KEPTN_SLI}",'dynatrace/sli.yaml')
          keptn.keptnAddResources("${KEPTN_SLO}",'slo.yaml')
          keptn.keptnAddResources("${KEPTN_DT_CONF}",'dynatrace/dynatrace.conf.yaml')          
        }
      }
...
````
## Step 3: Review the SLI,SLO definitions

Go into `carts\keptn` folder and review the files used to define the SLO. You can find more information about SLO definitions [here](https://keptn.sh/docs/0.7.x/quality_gates/slo/)

```
---
spec_version: "0.1.1"
comparison:
  aggregate_function: "avg"
  compare_with: "single_result"
  include_result_with_score: "pass"
filter:
objectives:
  - sli: "response_time_p95"
    pass:             # pass if (relative change <= 10% AND absolute value is < 600ms)
      - criteria:
          - "<=+10%"  # relative values require a prefixed sign (plus or minus)
          - "<600"    # absolute values only require a logical operator
    warning:          # if the response time is above 600ms and less or equal to 800ms, the result should be a warning
      - criteria:
          - "<=800"  # if the response time is above 800ms, the result should be a failure
  - sli: "response_time_p95_front-end"
    pass:
      - criteria:
          - "<=+10%"
          - "<1400"
    warning:
      - criteria:
          - "<=1500"
  - sli: "error_rate"
    pass:
      - criteria:
          - "<=+5%"
          - "<0.5"
    warning:
      - criteria:
          - "<5"
  - sli: "rt_addToCart" # looking at a particular transaction
    key_sli: true       # business critical transaction
    pass:
      - criteria:
          - "<=+10%"    # Degradation-driven
          - "<300000"   # NFR-driven
    warning:
      - criteria:
          - "<=+50%"
          - "<=500000"
total_score:
  pass: "90%"
  warning: "75%"
```

review the files used to define the SLI. You can find more information about Dynatrace SLI definitions using the Metrics V2 API [here](https://www.dynatrace.com/support/help/dynatrace-api/environment-api/metric-v2/)

```
---
spec_version: '1.0'
indicators:
  throughput:                  "metricSelector=builtin:service.requestCount.total:merge(0):sum&entitySelector=tag(environment:$STAGE),tag(app:$SERVICE),type(SERVICE)"
  error_rate:                  "metricSelector=builtin:service.errors.total.count:merge(0):avg&entitySelector=tag(environment:$STAGE),tag(app:$SERVICE),type(SERVICE)"
  response_time_p50:           "metricSelector=builtin:service.response.time:merge(0):percentile(50)&entitySelector=tag(environment:$STAGE),tag(app:$SERVICE),type(SERVICE)"
  response_time_p90:           "metricSelector=builtin:service.response.time:merge(0):percentile(90)&entitySelector=tag(environment:$STAGE),tag(app:$SERVICE),type(SERVICE)"
  response_time_p95:           "metricSelector=builtin:service.response.time:merge(0):percentile(95)&entitySelector=tag(environment:$STAGE),tag(app:$SERVICE),type(SERVICE)"
  response_time_p95_front-end: "metricSelector=builtin:service.response.time:merge(0):percentile(95)&entitySelector=tag(environment:$STAGE),tag(app:front-end),type(SERVICE)"
  rt_addToCart:                "metricSelector=calc:service.itemscontroller.requestresponsetime:filter(eq(requestname,addToCart)):merge(0):percentile(95)&entitySelector=tag(environment:$STAGE),tag(app:$SERVICE),type(SERVICE)"

```

## Step 2: Set the keptn variables inside Jenkins

You can retrieve the variables set in the last lab using

```
(bastion)$ export KEPTN_API_TOKEN=$(kubectl get secret keptn-api-token -n keptn -ojsonpath={.data.keptn-api-token} | base64 --decode)
(bastion)$ echo $KEPTN_API_TOKEN
(bastion)$ export KEPTN_BRIDGE=http://$(kubectl -n keptn get service api-gateway-nginx -ojsonpath='{.status.loadBalancer.ingress[0].ip}')/bridge
(bastion)$ echo $KEPTN_BRIDGE
(bastion)$ export KEPTN_ENDPOINT=http://$(kubectl -n keptn get service api-gateway-nginx -ojsonpath='{.status.loadBalancer.ingress[0].ip}')/api
(bastion)$ echo $KEPTN_ENDPOINT
```

Then inside Jenkins go into Manage `Jenkins > Configure System > Global properties` a set the variables values.

![keptn](./assets/keptn-variables.png)

