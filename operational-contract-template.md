# Operational Contract

> Customize this template based on the service's complexity and criticality.
> 
> Remove sections that are not relevant to the service.
> 
> ★ = Critical / Required field

**Last Updated:** `<YYYY-MM-DD>`

**Contract Version:** `<Version number, e.g. 1.0>`

---

## 1. Service Overview

|Field|Value|
|---|---|
|★ Service Name|`<Unique name of the service>`|
|★ Workload Type|`<HTTP API / gRPC / Worker / CronJob / Consumer / Other>`|
|★ Criticality|`<Low / Medium / High / Critical>`|
|★ Team / Owner|`<Team or person responsible for the service>`|
|Repository|`<URL of the source code repository>`|

---

## 2. Build & Runtime

| Field                      | Value                                                                              |
| -------------------------- | ---------------------------------------------------------------------------------- |
| ★ Dockerfile Location      | `<Path to the Dockerfile relative to the repository root>`                         |
| Base Image                 | `<Base container image and version/tag>`                                           |
| Image Name                 | `<Image name and tag after build>`                                                 |
| Build Args Required?       | `<Yes / No — if yes, list or reference the required build arguments>`              |
| Non-root User?             | `<Yes / No — specify the user if applicable>`                                      |
| ★ Health Check Endpoint    | `<Endpoint used to determine whether the application is alive>`                    |
| ★ Readiness Check Endpoint | `<Endpoint used to determine whether the application is ready to receive traffic>` |
| ★ Startup Time (approx)    | `<Expected time for the application to become ready>`                              |

---

## 3. Ports & Protocols

List every port exposed by the application and explain how each port is used.

|Port|Protocol|Purpose|Exposed to Cluster?|Exposed Externally?|Container Port Name|
|---|---|---|---|---|---|
|`<Port>`|`<HTTP / HTTPS / TCP / UDP / gRPC / Other>`|`<Purpose of this port>`|`<Yes / No>`|`<Yes / No>`|`<Container port name>`|
|`<Port>`|`<Protocol>`|`<Purpose>`|`<Yes / No>`|`<Yes / No>`|`<Name>`|
|`<Port>`|`<Protocol>`|`<Purpose>`|`<Yes / No>`|`<Yes / No>`|`<Name>`|

> Document whether the application listens on IPv4, IPv6, or both if this is operationally relevant.

---

## 4. Ingress / External Access

| Field                   | Value                                                   |
| ----------------------- | ------------------------------------------------------- |
| ★ Needs Ingress?        | `<Yes / No — specify why if relevant>`                  |
| ★ Target Port           | `<Port receiving external traffic>`                     |
| Host / Domain           | `<DNS hostname used to access the service>`             |
| Path Prefix             | `<URL path used to route traffic>`                      |
| TLS Required?           | `<Yes / No>`                                            |
| Rate Limiting Needed?   | `<Yes / No — describe limits if applicable>`            |
| CORS / Special Headers? | `<Yes / No — describe required headers or CORS policy>` |

> Document any special routing, authentication, rewrite, timeout, or proxy requirements.

---

## 5. Dependencies

Document all dependencies required for the service to function correctly.

### 5.1 Internal Services

List services that are called by this service inside the organization or cluster.

|Service Name|Namespace|★ Required?|Endpoint|Timeout / Retry|
|---|---|---|---|---|
|`<Service name>`|`<Namespace>`|`<Yes / No>`|`<Service endpoint>`|`<Timeout and retry behavior>`|
|`<Service name>`|`<Namespace>`|`<Yes / No>`|`<Service endpoint>`|`<Timeout and retry behavior>`|
|`<Service name>`|`<Namespace>`|`<Yes / No>`|`<Service endpoint>`|`<Timeout and retry behavior>`|

---

### 5.2 Databases

Document every database the service directly depends on.

|Name|Type|★ Required at Startup?|Connection / Secret Ref|Notes|
|---|---|---|---|---|
|`<Database name>`|`<PostgreSQL / MySQL / MongoDB / Redis / Other>`|`<Yes / No>`|`<Connection reference or Secret name>`|`<Purpose and operational notes>`|
|`<Database name>`|`<Database type>`|`<Yes / No>`|`<Connection reference or Secret name>`|`<Purpose and operational notes>`|

> Specify whether the database is required for startup, required only for specific features, or optional.

---

### 5.3 Cache

Document cache systems used by the service.

|Name|Type|★ Required at Startup?|Connection / Secret Ref|Notes|
|---|---|---|---|---|
|`<Cache name>`|`<Redis / Memcached / Other>`|`<Yes / No>`|`<Connection reference or Secret name>`|`<Purpose and behavior if unavailable>`|
|`<Cache name>`|`<Cache type>`|`<Yes / No>`|`<Connection reference or Secret name>`|`<Purpose and behavior if unavailable>`|

---

### 5.4 Message Queues / Event Brokers

Document Kafka topics, queues, or other messaging dependencies.

|Name|Type|Topic / Queue|Role|
|---|---|---|---|
|`<Broker name>`|`<Kafka / RabbitMQ / Other>`|`<Topic or queue name>`|`<Producer / Consumer / Producer & Consumer>`|
|`<Broker name>`|`<Broker type>`|`<Topic or queue name>`|`<Role>`|

> If the service consumes messages, document important consumer behavior such as offset handling, retry policy, dead-letter behavior, and ordering requirements.

---

### 5.5 External APIs

Document external systems or third-party APIs required by the service.

|Name|Endpoint|Auth Method|Notes|
|---|---|---|---|
|`<API name>`|`<API endpoint>`|`<API Key / OAuth / mTLS / None / Other>`|`<Purpose and failure behavior>`|
|`<API name>`|`<API endpoint>`|`<Authentication method>`|`<Purpose and failure behavior>`|

---

### ★ Failure Behavior

Describe what happens when each critical dependency becomes unavailable.

- `<Dependency>` unavailable → `<Application behavior>`
    
- `<Dependency>` unavailable → `<Application behavior>`
    
- `<Dependency>` unavailable → `<Application behavior>`
    
- `<Dependency>` unavailable → `<Application behavior>`
    

> Explicitly state whether the service fails to start, continues with degraded functionality, retries, queues work, or returns errors to callers.

---

## 6. Configuration & Environment Variables

Document all environment variables required to build, deploy, or operate the service.

|Variable|★ Required?|Default|Description|Secret?|
|---|---|---|---|---|
|`<VARIABLE_NAME>`|`<Yes / No>`|`<Default value or —>`|`<What this variable controls>`|`<Yes / No>`|
|`<VARIABLE_NAME>`|`<Yes / No>`|`<Default value or —>`|`<What this variable controls>`|`<Yes / No>`|
|`<VARIABLE_NAME>`|`<Yes / No>`|`<Default value or —>`|`<What this variable controls>`|`<Yes / No>`|
|`<VARIABLE_NAME>`|`<Yes / No>`|`<Default value or —>`|`<What this variable controls>`|`<Yes / No>`|

> Do not place actual secret values in this document. Reference the Secret or external secret-management system instead.

---

## 7. ConfigMaps & Volumes

Document configuration files, persistent storage, and temporary volumes used by the service.

|Type|Required?|Name / Source|Mount Path|Notes|
|---|---|---|---|---|
|`<ConfigMap / Secret / PVC / EmptyDir / Other>`|`<Yes / No>`|`<Resource name or source>`|`<Container mount path>`|`<Purpose and operational notes>`|
|`<Type>`|`<Yes / No>`|`<Resource name or source>`|`<Mount path>`|`<Purpose and operational notes>`|
|`<Type>`|`<Yes / No>`|`<Resource name or source>`|`<Mount path>`|`<Purpose and operational notes>`|

> For persistent storage, document what data is stored and whether the data must survive pod or container replacement.

---

## 8. Secrets Management

Document how sensitive configuration and credentials are managed.

|Field|Value|
|---|---|
|★ Secrets Required?|`<Yes / No>`|
|Secret Keys|`<List of required secret keys or references>`|
|Management Method|`<Kubernetes Secret / External Secrets Operator / Vault / Other>`|
|Rotation Needed?|`<Yes / No — specify rotation requirements if applicable>`|

> Never store actual secret values, passwords, tokens, or private keys in this document.

---

## 9. Testing

Document the tests that must pass before deployment.

|Field|Value|
|---|---|
|★ Tests Required Before Deploy?|`<Yes / No>`|
|How to Run Unit Tests|`<Command used to run unit tests>`|
|How to Run Integration Tests|`<Command used to run integration tests>`|
|Test Command (CI)|`<Command used by CI/CD>`|
|Needs Test DB / Services?|`<Yes / No — list required services>`|
|Coverage Threshold|`<Minimum required coverage, if applicable>`|

### Additional Testing Notes

1. `<Describe any required test environment setup.>`
    
2. `<Describe required dependencies or test data.>`
    
3. `<Describe conditions that must be satisfied before deployment.>`
    

---

## 10. Observability

### 10.1 Metrics

Document the metrics exposed by the service and the metrics that should be monitored or alerted on.

|Field|Value|
|---|---|
|★ Exposes Metrics?|`<Yes / No>`|
|Metrics Path|`<Metrics endpoint, e.g. /metrics>`|
|Metrics Port|`<Port used for metrics>`|
|★ Key Metrics to Alert On|`<List of important metrics and alert conditions>`|
|SLO / Latency Target|`<SLO, SLA, latency target, or other performance objective>`|

> Include application-level metrics that are important for determining service health, not only infrastructure metrics.

---

### 10.2 Logging

|Field|Value|
|---|---|
|★ Log Format|`<JSON / Plain Text / Other>`|
|Important Fields|`<Fields required for troubleshooting, correlation, and incident response>`|

> Document important identifiers such as request IDs, trace IDs, user IDs, transaction IDs, or other correlation fields when applicable.

---

### 10.3 Tracing

|Field|Value|
|---|---|
|OTel Instrumented?|`<Yes / No / Planned>`|
|Propagator|`<W3C TraceContext / B3 / Other / None>`|

> Document any special tracing configuration, sampling requirements, or collector dependencies.

---

## 11. Resource Requirements & Scaling

Document the resources required by the workload and how it scales.

|Field|Value|
|---|---|
|★ CPU Request|`<Minimum CPU requested by the workload>`|
|★ CPU Limit|`<Maximum CPU the workload can consume>`|
|★ Memory Request|`<Minimum memory requested by the workload>`|
|★ Memory Limit|`<Maximum memory the workload can consume>`|
|★ GPU Required?|`<Yes / No — specify GPU requirements if applicable>`|
|Min Replicas|`<Minimum number of running replicas>`|
|Max Replicas|`<Maximum number of running replicas>`|
|Scaling Metric|`<CPU / Memory / Queue Length / Custom Metric / Other>`|
|HPA Target|`<Target value used for autoscaling>`|
|PodDisruptionBudget|`<Yes / No — specify configuration if applicable>`|
|Pod Anti-Affinity|`<Yes / No — describe scheduling requirements>`|
|Safe to run multiple replicas?|`<Yes / No — explain state or concurrency limitations>`|

> Document any stateful behavior, local storage dependency, leader-election requirement, singleton requirement, or other constraint that affects horizontal scaling.

---

## 12. Scheduling (CronJob / Worker only)

> Remove this section if the service is not a scheduled workload or worker.

|Field|Value|
|---|---|
|Schedule|`<Cron expression or scheduling mechanism>`|
|Concurrency Policy|`<Allow / Forbid / Replace / Not applicable>`|
|Timeout|`<Maximum execution time>`|
|Retry on Failure?|`<Yes / No — describe retry behavior>`|
|Successful Job History|`<Number of successful jobs to retain>`|
|Failed Job History|`<Number of failed jobs to retain>`|

> Document any operational requirements related to job overlap, missed schedules, retries, or manual execution.

---

## 13. Security & Compliance

Document security-related runtime and network requirements.

| Field                         | Value                                                       |
| ----------------------------- | ----------------------------------------------------------- |
| Runs as Non-Root?             | `<Yes / No>`                                                |
| ReadOnly Root Filesystem?     | `<Yes / No>`                                                |
| Drop All Capabilities?        | `<Yes / No>`                                                |
| Network Policies Needed?      | `<Yes / No — describe allowed communication if applicable>` |
| PII / Sensitive Data Handled? | `<Yes / No — describe the type of data if applicable>`      |
| Compliance Requirements       | `<None / List applicable compliance requirements>`          |

> Document any additional security requirements such as mTLS, image signing, vulnerability scanning, encryption, or restricted network access.

---

## 14. Deployment Notes

Document operational requirements and risks related to deployment.

|Field / Notes|Value|
|---|---|
|★ Runs DB Migrations on Startup?|`<Yes / No — describe migration behavior>`|
|★ Graceful Shutdown Timeout|`<Time allowed for graceful shutdown>`|
|Startup Order Dependencies|`<Dependencies that must be ready before the service starts>`|
|★ Rollback Considerations|`<Conditions or limitations that affect rollback>`|
|Known Issues / Quirks|`<Known operational issues, limitations, or special behavior>`|

> Explicitly document whether a deployment can be safely rolled back after database schema changes or other irreversible operations.

---

## 15. Incident Response Notes

Document common failure scenarios and the recommended first response.

|Scenario|Recommended Action|Notes|
|---|---|---|
|`<Failure scenario>`|`<First troubleshooting or mitigation action>`|`<Additional context>`|
|`<Failure scenario>`|`<First troubleshooting or mitigation action>`|`<Additional context>`|
|`<Failure scenario>`|`<First troubleshooting or mitigation action>`|`<Additional context>`|
|`<Failure scenario>`|`<First troubleshooting or mitigation action>`|`<Additional context>`|

> Focus on information that helps an engineer who is on-call and may not be familiar with the service.

---

## 16. Contact & On-Call

Document who owns the service and where operational support can be found.

|Role|Contact|
|---|---|
|★ Primary Owner|`<Team, person, or contact channel>`|
|On-Call Escalation|`<On-call team, rotation, or contact channel>`|
|Runbook|`<URL to the operational runbook>`|

---

## 17. Additional Notes

Use this section for operational information that does not fit into the sections above.

- `<Additional operational requirement>`
    
- `<Known limitation>`
    
- `<Special deployment or maintenance requirement>`
    
- `<Other relevant information>`
    

> Any change to ports, dependencies, environment variables, resource requirements, deployment behavior, or other operational characteristics should also update this document.
