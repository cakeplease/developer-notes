The ability to understand the state of a system by looking at the logs, metrics abd traces it produces. See [[Monitoring]]

1. **Logs** - Logs are a record of what has happened in your application. They are useful for debugging, but due to their unstructured format they generally do not scale very well.

2. **Metrics** - Metrics are a numerical measurement of something in your application. They are useful for understanding the performance of your application and is generally more scalable than logs both in terms of storage and querying since they are structured data.

3. **Traces** - Traces are a record of the path a request takes through your application. They are useful for understanding how a request is processed in your application.


# NAIS APM
Nais APM is an app in your team's Grafana that gives every Nais service a single home for application performance monitoring: a health overview, an issues list across frontend _and_ backend errors, endpoint and database analytics, traces, and logs — built on the telemetry your apps already send to the platform.

![[Pasted image 20260908100736.png]]