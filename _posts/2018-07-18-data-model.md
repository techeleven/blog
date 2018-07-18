---
layout: post
title: "Data Model of the tech11 Insurance Platform"
date: 2018-07-18 10:38:10 +0200
tags: blog 
lang: en
author: matthias
---

![Data Model of the tech11 Insurance Platform](/assets/data-model/data-model.png)

  
Within the **[tech11] Business Workbench** the insurance product model is defined with the **Product Designer**.

In this diagram we show a product model for *traditional* insurance products. The model is based on the German GDV data model that defines
*Sales Product*, *Product* and *Basic Product*. Here the basic product is the smallest selectable unit that is also linked to a calculated premium.

> The tech11 Insurance Platform provides also the possibility to exchange this product model to other models. 
> For example, in case of situative insurance products maybe a smaller product structure is more suitable.

## Product -> Policy
The insurance product model defines the structure of the stored contract data including its attributes, rules, validations, etc..

## Policy -> Accounting Records
The contract module contains the data for a 100% premium. The 100% premium is the premium that is typically valid for one insurance year or in general for a defined period.  
This premium is the basic for the accounting records where the 100% premium is split by a p.r.t. calculation regarding the payment period and the main due date frame.

## Accounting Records -> Regulatory
The accounting record that is based on the basic product definition is always linked to an insurance branch that defines also the current tax rates. Based on this data the authority reports are generated.

## Coverage -> Subclaim
A basic product contains x coverages. For each coverage there can be defined within the product designer a limit, a deductible, conditions, initial reserves, etc.
In case of a damage, the claim is checked against the coverages. Furthermore the happening could be affect different coverages in different contract modules and even in different contracts. Therefore a happening is linked to a *claim* and the concrete coverages of a contract module are linked to sub claims.

- - - 

# References / Connections

Although if it sounds that the data are linked between the different modules that's not the case. Each Microservice contains his own data source (database).
Referential integrity is not give by the used Microservice architecture.

Fortunately, the tech11 Insurance Platform follows an *only-insert-pattern* where no data are manipulated or deleted. Therefore a given *reference id* is always be available.

# Detail Level

This diagram is just a helicopter view of the tech11 Insurance Platform.


[tech11]:   https://tech11.com/en/products
