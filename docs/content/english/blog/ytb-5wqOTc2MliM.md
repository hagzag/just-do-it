---
title: "Scaling I/O Bound Microservices"
meta_title:
description:
date: 2020-03-04T09:21:00Z
image: "https://i.imgur.com/4Aaf6O3.png"
categories: ["Development", "Developer Experience (DevEx)", "Presentations", "Webinar", "Kubernetes", "Youtube", "Production Readiness"]
author: "Haggai Philip Zagury (hagzag)"
tags: ["Webinar", "Production Readiness", "Youtube", "DevEx"]
draft: false
---

In this meetup, we will continue our #2ndhalf journey to the next^2.
You can see the talks from the 1st meetup of this series here - http://bit.ly/second-half-p1
Nowadays, scaling and auto-scaling have become relatively easy tasks. Everyone knows how to set up auto-scaling environments - Auto-Scaling groups, Swarm, Kubernetes, etc.

But when we try to scale I/O Bound workloads:
Message queues (Kafka, Rabbit, NATS)
Distributed databases (Hadoop, Cassandra)
Storage subsystems (CEPH, GlusterFS, HDFS),
the traditional auto-scaling mechanisms are just not enough.

Heavy calculations must be performed to determine the I/O bottlenecks. Rebalancing the data after a scaling event can take up to hours depending on your data & could, resulting in data loss if not properly designed.

We will deep dive into this type of workload and walk you through code samples you can apply in your own environment.

## Video

{{< youtube 5wqOTc2MliM >}}

<hr>

## Presntation slides

<iframe src="https://www.slideshare.net/slideshow/embed_code/key/kGICkp3c1LZQj8?startSlide=1" width="800" height="600" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px;max-width: 100%;" allowfullscreen></iframe><div style="margin-bottom:5px"><strong><a href="https://www.slideshare.net/slideshow/scaling-io-bound-microservices/227182158" title="Scaling i/o bound Microservices" target="_blank">Scaling i/o bound Microservices</a></strong> from <strong><a href="https://www.slideshare.net/hagzag" target="_blank">Haggai Philip Zagury</a></strong></div>
