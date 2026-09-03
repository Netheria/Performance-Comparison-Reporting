# Performance Testing Comparison Report

> **Automatically generated performance analysis - not a manually assembled report.**
>
> Build v2 is compared with Build v1 to demonstrate how performance-test data can be transformed into a structured, interactive, decision-ready report.

<p align="center">
  <a href="https://Netheria.github.io/Performance-Comparison-Reporting/"><strong>🚀 OPEN THE LIVE REPORT</strong></a>
</p>

<p align="center">
  <sub>Synthetic data · Representative core · Build-to-build comparison</sub>
</p>

<video src="assets/Preview.mov" autoplay loop muted playsinline align="center" width="100%"></video>

---

## What is this?

**The analytical report is the main artifact of any performance test.**

This repository demonstrates an **automatically generated HTML report for performance and stability comparison**.

The ideas are simple:

> **Performance testing should not end with a pile of raw metrics.**

The collected data should be converted into something that can be reviewed, explained, and used to make a deployment decision.

> **The report should not be prepared manually during the month.**

Instead of manually assembling tables, charts, observations, anomaly notes, and conclusions after every test run, the reporting layer generates them from the collected test data.

### 👀 See it first

The report is designed to be explored interactively rather than read as a static document: expand transaction groups, switch between data views, inspect charts, compare builds, and read the generated conclusions.

---

## What does the example demonstrate?

The example covers the core of a performance-comparison workflow without attempting to include every metric that the underlying performance-testing framework can produce.

It demonstrates:

- **Build-under-test vs reference-build comparison**
- Aggregate performance metrics
- Transaction-level performance analysis
- Response-time distribution and variability analysis
- Throughput comparison
- Resource-consumption analysis
- Test anomaly observations
- Stability-oriented meta metrics
- Section-level conclusions
- A final **GO / NO-GO style deployment assessment**

The report deliberately uses a **reduced but representative metric surface**.

The purpose is to demonstrate the reporting approach, not to claim that these are the only metrics a real implementation should contain.

**THE REAL REPORT CAN BE EXTENDED WITH ANYTHING.**

---

## Why build a custom report?

A standard performance-tool summary is useful for answering questions such as:

> How many requests were executed?
>
> What was the average response time?
>
> What was the 90th percentile?

Those numbers are necessary, but they are often not enough to explain:

- **what changed**

- **where it changed**

- **whether the change is consistent**

- **whether the build should move forward**

This example treats reporting as a separate engineering problem:

**Raw performance data → statistical comparison → interpretation → decision-ready report**

The report, therefore, brings several analytical layers together instead of leaving the reviewer to manually connect them.

---

## Example scenario

The report compares two builds of the same application:

| | Build v1 | Build v2 |
|---|---|---|
| Role | Build under test | Reference build |
| Purpose | Candidate release | Baseline for comparison |
| Workload | Comparable test workload | Comparable test workload |
| Outcome | **NO-GO in this example** | - |

The synthetic dataset was constructed to demonstrate a realistic **regression story** rather than an idealized success case.

Build v2 shows degradation across several areas while remaining operationally stable.

The result is intentionally more interesting than a simple “everything failed” scenario: the report has to distinguish between isolated improvements, transient anomalies, broader regressions, and findings that matter enough to affect the final deployment decision.

The report ultimately concludes that Build v2 should not be promoted in its current state. Among the highlighted regressions are slower agent-message processing, slower workflow processing, lower overall throughput, higher resource consumption in several components, and increased variability.

---

## Important limitations

This repository is a **demonstration of the reporting concept**, not a production benchmark.

### Synthetic data

The report data is synthetic and was created to reproduce believable performance-test behavior and provide a meaningful comparison scenario.

It should **not** be treated as evidence about the performance of a real production system.

### Representative core

The example intentionally contains only a subset of the broader metric and reporting capabilities available in the underlying performance-testing framework.

The goal is to show the **core reporting pattern** without turning the example into an enormous collection of every possible metric.

### Build-to-build comparison

The primary comparison is:

**Build under test ↔ reference build**

This is different from evaluating a build directly against universal performance limits.

The report can be adapted to an **expected-value / threshold / target model** when such a reference model exists.

In that case, the expected dataset can act as the comparison target instead of another software build.

---

## Report walkthrough

### 1. Intro information

The report begins with the context required to understand the comparison.

It provides build identification, infrastructure information, and test configuration for both builds.

The example includes component image/version information, CPU and memory configuration, restart counts, agent/client counts, ramp-up settings, and time under load.

This section answers the first question a reviewer should have:

> **What exactly am I comparing?**

---

### 2. Performance metrics

The main analytical section is divided into several layers.

#### Transaction groups

Transactions are organized into logical groups rather than presented as one undifferentiated list.

The example contains groups for:

- Database query transactions
- Create Agents transactions
- Log In transactions
- Dashboard transactions
- Workflow Actions transactions
- Messaging transactions

This gives the report a business/functional structure while retaining access to individual API and workflow transactions.

#### Summary

The summary provides aggregate-level comparison between the two builds.

The report supports multiple representations of the same data, including **Interval** and **Period** bucketing views.

Tables, aggregate charts, transaction breakdowns, and generated conclusions are presented together.

This is intended to answer:

> **Is the new build broadly better, worse, or mixed?**

#### Transaction data

The report then drills down to individual transactions.

This makes it possible to move from:

**“the group got slower”**

to:

**“these specific operations account for the regression.”**

The report can also identify situations where one build has no corresponding execution data and explicitly flag the discrepancy for investigation instead of silently treating it as a normal result.

#### Spread / variability

Absolute response time is only part of the picture.

The example also compares response-time variability and highlights cases where performance became less predictable, even when average values alone might not look dramatic.

That distinction matters in regression analysis because a build can become **slower, more volatile, or both**.

#### Resource consumption

The report connects application-level performance with infrastructure behavior.

Resource sections include time-series views and generated observations for resources such as CPU and memory.

This supports questions such as:

> Did the regression occur together with higher resource consumption?

> Is a latency increase isolated, or does it coincide with a resource change?

---

### 3. Test anomalies

The anomaly section is intentionally different from the metric comparison.

It looks for unusual runtime behavior that deserves attention even when it does not amount to a deployment blocker by itself.

In the example, the report identifies transient Engine CPU spikes, an Engine memory excursion, repeated variability in Agent Messages, messaging spread spikes, and transient database-connection peaks.

It also explicitly notes the absence of pod restarts and error growth in the available data.

The important distinction is:

**anomaly ≠ automatic failure**

An anomaly is evidence that something happened and may require investigation. Its severity depends on the broader context.

---

### 4. Stability meta metrics

The report also contains product-specific stability indicators that are not meaningful in isolation but become useful when correlated with performance data.

The example includes agent activity and database-connection-related observations.

This provides another analytical layer:

**Performance metrics + system behavior + resource data + anomalies**

rather than looking at latency in isolation.

---

### 5. Ending conclusions

The final section converts the detailed analysis into a stakeholder-readable decision.

For the example dataset, the report produces a **NO-GO** verdict and explains why.

It highlights principal regressions, resource concerns, consistency concerns, positive findings, stability observations, and recommended next steps.

The intention is that a **stakeholder should not need a separate meeting just to understand the result**.

The detailed sections remain available for engineers who want to investigate further.

---

## A closer look at the interactive report

The HTML is designed as an interactive analysis document rather than a static export.

It includes:

- Tabbed build comparison
- Collapsible transaction groups
- Tabbed metric representations
- Chart-based visualization
- Interval / Period representation modes switching
- Period timespan switching
- Expandable table and conclusion views
- Interactive chart width controls
- Inline metric glossary/tooltips
- Navigation between major report sections

The implementation uses a custom HTML template and client-side JavaScript components for the interactive behavior.

The current example is generated from a custom backend/Velocity reporting template and uses libraries such as Bootstrap and Chart.js.

---

## Automation is the point

The central idea behind this repository is not the visual styling of the HTML.

It is the **automation of the entire reporting step**.

A useful reporting pipeline should be able to take structured performance-test results and automatically produce:

```text
Test execution data
        ↓
Metric aggregation
        ↓
Build-to-build comparison
        ↓
Transaction-level analysis
        ↓
Resource / stability correlation
        ↓
Section conclusions
        ↓
Anomaly observations
        ↓
Final deployment assessment
        ↓
Ready interactive HTML report
```

That is the capability this repository is intended to showcase.

The practical benefit is straightforward: a rich report does not need to be manually reconstructed after every execution.

---

## Relationship to the performance-testing frameworks

This repository is intentionally focused on the **reporting and analysis side** of performance engineering.

The related framework projects demonstrate how the performance-test data can be generated and collected; this repository demonstrates what can be done with that data afterward.

In other words:

```text
Performance test framework
        ↓
Raw / structured performance data
        ↓
Comparison & analysis layer
        ↓
Decision-ready report
```

The report is, therefore, not intended to replace the performance-testing framework.

It represents the stage that comes **after the test execution**.

---

## What this project demonstrates

> **The output is not just data visualization. It is an automatically generated performance assessment.**

From a Performance Engineering perspective, the project demonstrates the ability to think beyond a single response-time number and build a reporting flow around:

- Comparison rather than isolated measurements
- Aggregate and transaction-level analysis
- Variability, not only averages
- Resource and runtime context
- Anomaly interpretation
- Automated conclusions
- Stakeholder-oriented communication

---

## Related projects

### k6 Performance Testing Framework

A more technically extensive performance-testing framework demonstrating workload execution, stateful scenarios, observability, result collection, and reporting integration.

**[Open the k6 framework repository →](https://github.com/Netheria/k6-Performance-Testing-Framework)**

### JMeter Performance Testing Framework

The earlier version of the performance-testing framework demonstrating the preceding implementation approach.

**[Open the JMeter framework repository →](https://github.com/Netheria/JMeter-Performance-Testing-Framework)**

### Performance Testing Strategy

A generalized portfolio-oriented strategy describing how performance testing can be approached before concrete execution and analysis begin.

**[Open the Performance Testing Strategy repository →](https://github.com/Netheria/Performance-Testing-Strategy)**

---

## Final note

A performance report should help people answer more than:

> “What were the numbers?”

It should help answer:

> **What changed?**
>
> **Where did it change?**
>
> **How consistent is the change?**
>
> **What else changed around it?**
>
> **Does it matter?**
>
> **Should this build move forward?**

This repository is an example of automating that path from **performance-test data to an explainable deployment decision**.

**[🚀 Open the live report →](https://Netheria.github.io/Performance-Comparison-Reporting/)**
