---
layout: post
title:  "AWS Monitoring Solutions: CloudWatch"
date:   2025-03-10
categories: [aws]
tags: [cloud, monitoring]
---
Monitoring is a crucial feature that allows to see how the different components of an architecture are handling operational workloads on real time.

Data for monitoring can come from various sources (all services generate operational data called metrics. Metrics over time are called statistics.)

Examples of metrics:

- CPU Utilization
- Network Traffic (In and Out)
- Number and size of objects stored in an S3 bucket

A Baseline is a reference point for any given metric. If a metric deviates from the baseline, you know something is wrong.

The AWS monitoring solution is CloudWatch. It aggregates metrics from all AWS services into a single source of truth you can use to monitor your solutions.

**CloudWatch**
