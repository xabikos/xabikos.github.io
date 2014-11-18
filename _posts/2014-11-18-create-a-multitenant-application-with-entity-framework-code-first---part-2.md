---
layout: post
title: "Create a multitenant application with Entity Framework Code First - Part 2"
date: 2014-11-18 20:15:00
description: Create infrastructure code to achieve multitenancy in an application by using Entity Framework Code First
categories: [multitenant, application design, software as a service]
tags: [entity framework, multi-tenant, interceptors, code first]
fullview: false
comments: true
shortinfo: In continuation of Part 1 of creating a multitenant application with Entity Framework Code First we are going to see how we can use Interceptors to apply filtering when querying the data in a transparent way for our application.
---

In continuation of [Part 1]({% post_url 2014-11-17-create %}) of creating a multitenant application with Entity Framework Code First we are going to see how we can use Interceptors to apply filtering when querying the data in a transparent way for our application.