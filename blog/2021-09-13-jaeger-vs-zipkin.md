---
title: Jaeger vs Zipkin - Key differences, use-cases and alternatives
slug: jaeger-vs-zipkin
date: 2021-09-13
tags: [jaeger, apm-tools]
author: Ankit Anand
author_title: SigNoz Team
author_url: https://github.com/ankit01-oss
author_image_url: https://avatars.githubusercontent.com/u/83692067?v=4
description: Jaeger and Zipkin are two popular open-source projects used for end-to-end distributed tracing. WHile Zipkin is an older project and a wider community, Jaeger has modern, scalable architecture and supports open standards of instrumentation libraries..
image: /img/blog/2021/09/jaeger_vs_newrelic_cover-min.jpg
keywords:
  - jaeger
  - zipkin
  - distributed tracing
  - traces
---

Distributed tracing is becoming a critical component of any application's performance monitoring stack. Setting it up in-house is a hearculean task, and that's why many companies prefer outside tools. Jaeger and Zipkin are two popular open-source projects used for end-to-end distributed tracing. Let us explore their key differences in this article.

<!--truncate-->

![Cover Image](/img/blog/2021/09/jaeger_vs_zipkin_apm_cover-min.jpg)

Both Zipkin and Jaeger are popular open-source distributed tracing tool. Zipkin was orginally inspired by Google's Dapper and was developed by Twitter. Zipkin is a much older project than Jaeger and was first released as an open-source project in 2012. Jaeger was originally built by teams at Uber and then open-sourced in 2015. It got accepted as a Cloud Native incubation project in 2017 and graduated in 2019.

Before we dive into the differences between Jaeger and Zipkin, let's take a short detour to understand what distributed tracing is.

## What is distributed tracing?
In the world of microservices, a user request travels through hundreds of services before serving a user what they need. To make a business scalable, engineering teams are responsible for particular services with no insight into how the system performs as a whole. And that's where distributed tracing comes into the picture.

import Screenshot from "@theme/Screenshot"

<Screenshot
    alt="Microservices architecture"
    height={500}
    src="/img/blog/2021/08/jaeger_ui-min.png"
    title="Microservice architecture of a fictional e-commerce application"
    width={700}
/>

Distributed tracing gives you insight into how a particular service is performing as part of the whole in a distributed software system. There are two important concepts involved in distributed tracing: **Spans** and **trace context**.

User requests are broken down into spans.

> What are spans?<br></br>
> Spans represent a single operation within a trace. Thus, it represents work done by a single service which can be broken down further depending on the use case.

A trace context is passed along when requests travel between services, which tracks a user request across services. You can see how a user request performs across services and identify what exactly needs your attention without manually shifting through multiple dashboards.

<Screenshot
    alt="Trace context is passed to track user requests across services"
    height={500}
    src="/img/blog/2021/09/opentelemetry_distributed_tracing-min.png"
    title="A trace context is passed when user requests passes from one service to another"
    width={700}
/>

## Jaeger and Zipkin: Key components
[Jaeger's](https://github.com/jaegertracing/jaeger) source code is primarily written in Go, while [Zipkin's](https://github.com/openzipkin/zipkin) source code is primarily written in Java. The architecture of Jaeger and Zipkin is somewhat similar. Major components in both architectures include:

- Instrumentation Libraries
- Collectors
- Query Service and web UI
- Database Storage

<Screenshot
    alt="Jaeger architecture"
    height={500}
    src="/img/blog/2021/09/Jaeger_architecture-min.jpg"
    title="Illustration of  Jaeger architecture (Source: Jaeger website)"
    width={700}
/>

<Screenshot
    alt="Zipkin architecture"
    height={500}
    src="/img/blog/2021/09/zipkin_architecture-min.jpg"
    title="Illustration of Zipkin architecture (Source: Zipkin website)"
    width={700}
/>

### Instrumentation Libraries
Instrumentation is the process of generating telemetry data(logs, metrics, and traces) from an application code. Both Jaeger and Zipkin provide language-specific instrumentation libraries. Instrumentation enables a service to create spans on incoming requests and to attach context information on outgoing requests.

List of officially supported client libraries of Jaeger and Zipkin:

Key differences to note about instrumentation libraries of Jaeger and Zipkin:

- Jaeger's instrumentation libraries are based on [OpenTracing APIs](https://opentracing.io/). OpenTracing was also started at Uber with an aim to create vendor-neutral instrumentation APIs for distributed tracing. Zipkin has its own instrumentation libraries.
- Jaeger has [official client libraries](https://www.jaegertracing.io/docs/1.26/client-libraries/) in Go, Java, Node.js, Python, C++, C#. Zipkin team maintains [instrumentation libraries](https://zipkin.io/pages/tracers_instrumentation.html) for frameworks in C#, Go, Java, Javascript, Ruby, Scala, and PHP.
- Both Jaeger and Zipkin support out-of-box instrumentation for a lot of popular frameworks. Jaeger is also compatible with Zipkin's API. That means you can use instrumentation libraries of Zipkin with Jaeger
J[aeger's 3rd party supported frameworks](https://github.com/orgs/opentracing-contrib/repositories)
[Zipkin's 3rd party supported frameworks](https://zipkin.io/pages/tracers_instrumentation.html)

### Collectors
Telemetry data collected by the instrumentation libraries are sent to a collector in both Jaeger and Zipkin. Jaeger's collectors validate traces, index them, perform any transformations, and finally stores them. Zipkin collector too validates and indexes the collected trace data for lookups.

### Query Service and Web UI
Zipkin provides a JSON API for finding and retrieving traces. Jaeger provides stateless service API endpoints which are typically run behind a load balancer, such as NGINX.

The consumer of the query service is a Web UI in both Jaeger and Zipkin, which is used to visualize trace data by a user.

<Screenshot
    alt="Jaeger's web UI showing Gantt charts"
    height={500}
    src="/img/blog/2021/08/jaeger_gantt_charts-min.png"
    title="Jaeger's Web UI showing spans with Gantt charts"
    width={700}
/>

<Screenshot
    alt="Zipkin trace UI"
    height={500}
    src="/img/blog/2021/09/jaeger_vs_zipkin_trace_ui.jpg"
    title="Zipkin's trace UI"
    width={700}
/>

### Database storage
Both Jaeger and Zipkin provide pluggable storage backends for trace data. Cassandra and Elasticsearch are the primarily supported storage backends by Jaeger.

Zipkin was originally built to store data in Cassandra, but it later started supporting Elasticsearch and MySQL too.

## Jaeger vs Zipkin: Key differences
Jaeger and Zipkin have a lot of similarities in their architecture. Though Zipkin is an older project, Jaeger has a more modern and scalable design. Let us summarize the key differences between Jaeger and Zipkin in the following points:

- Jaeger's has wider support of instrumentation libraries as it supports OpenTracing APIs and is also compatible with Zipkin's API. Jaeger also provides an option to [migrate from Zipkin](https://www.jaegertracing.io/docs/1.26/getting-started/#migrating-from-zipkin).
- Jaeger can be deployed as a single binary where all Jaeger backend components run as a single process or as a scalable distributed system. Zipkin, on the other hand, can only be run as a single binary that includes the collector, storage, query service and web UI.
- As Jaeger comes under CNCF along with other projects such as Kubernetes, there are official orchestration templates for running Jaeger with [Kubernetes](https://github.com/jaegertracing/jaeger-kubernetes) and [OpenShift](https://github.com/jaegertracing/jaeger-openshift). Zipkin provides three options to build and start an instance of Zipkin: using Java, Docker, or running from the source.
- Despite being older, Jaeger has caught upto Zipkin in terms of community support. Zipkin is a standalone project which came into existence before containerization went mainstream. Jaeger as part of CNCF is a recognized project in cloud-native architectures.

Both Jaeger and Zipkin are strong contenders when it comes to a distributed tracing tool. But are traces enough to solve all performance issues of a modern distributed application? The answer is no. You also need metrics and a way to correlate metrics with traces with a single dashboard. Most SaaS vendors provide both metrics and traces under a single pane of glass. But the beauty of Jaeger and Zipkin is that they are open-source. What if there is an open-source solution that does both and comes with great web UI with actionable insights for your engineering team?

That's where [SigNoz](https://signoz.io/) comes into the picture.

## A better to alternative to Jaeger and Zipkin - SigNoz
SigNoz is a full-stack open-source application performance monitoring and observability tool which can be used in place of Jaeger and Zipkin. It provides advanced distributed tracing capabilities along with metrics under a single dashboard.

SigNoz is built to support OpenTelemetry natively. It also provides users flexibility in terms of storage. You can choose between ClickHouse or Kafka + Druid as your backend storage while installing SigNoz.

<Screenshot
    alt="Architecture of SigNoz with OpenTelemetry and ClickHouse"
    height={500}
    src="/img/blog/2021/09/SigNoz_architecture_clickhouse.png"
    title="Architecture of SigNoz with ClickHouse as storage backend and OpenTelemetry for code instrumentatiion"
    width={700}
/>

SigNoz comes with out of box visualization of things like RED metrics.

<Screenshot
    alt="SigNoz UI showing the popular RED metrics"
    height={500}
    src="/img/blog/common/signoz_charts_application_metrics.png"
    title="SigNoz UI showing application overview metrics like RPS, 50th/90th/99th Percentile latencies, and Error Rate"
    width={700}
/>

Some of the things SigNoz can help you track:

- Application overview metrics like RPS, 50th/90th/99th Percentile latencies, and Error Rate
- Slowest endpoints in your application
- See exact request trace to figure out issues in downstream services, slow DB queries, call to 3rd party services like payment gateways, etc
- Filter traces by service name, operation, latency, error, tags/annotations.
- Run aggregates on trace data
- Unified UI for both metrics and traces

You can check out SigNoz's GitHub repo here 👇

[![SigNoz GitHub repo](/img/blog/common/signoz_github.png)](https://github.com/SigNoz/signoz)


