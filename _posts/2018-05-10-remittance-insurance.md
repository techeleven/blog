---
layout: post
title: "Remittance Insurance"
date: 2018-05-10 11:31:14 +0100
tags: remittance insurance, microinsurance, platform 
lang: en
author: matthias
---
## Background to Remittance Insurance

Remittances is a billion dollar business ([Wikipedia - Remittance]). 
Migrants sends money back to their poor families at home to support them to have just a better live.
But instead of sending only money, it could be better just to protect their families for different risks by issuing an insurance policy. A remittance insurance.

The paper [Microinsurance and Remittances] describes the as is situation and gives a very good overview to the problems and possible starting points to improve the situation.

![Purchasing remittance insurance](/assets/remittance-insurance/purchasing-remittance-insurance.png)
(Source: https://www.cimonline.de/static/media/giz2011-en-microinsurance-remittances.pdf)

### Indicated problems:

* Premium is paid annually
* High drop-out rates
* No "financial literacy"

## A Possible Approach: Embedded Microinsurance

* Move the insurance sales process directly to the remittance provider. 
    
    The insurance policy (for example a term life insurance) should be directly effected as part of the fee for the remittance. The migrant has nothing to do with all the processes around the issuing of a policy.

* Define business rules which effect an insurance policy

    * Example 1: Starting from a certain amount of money within a defined period
    * Example 2: Starting from a certain amount of remittances
    * Example 3: ...


## Technical Solution based on the tech11 Platform

For issuing a remittance microsinsurance we have implemented a sample show case by using the [tech11 insurance platform]. 
For this demo case we did the following configuration:

* Implement a BPMN2.0 remittance sales process
* Define busines rules with DMN1.1 that decides if an policy should be issued 
* Trigger the standard issue policy process (reference implementation policy-1000 from tech11's ICE module )

![BPMN process remittance insurance](/assets/remittance-insurance/bpmn-process-remittance-insurance-sales.png)
(BPMN2.0 remittance sales process)

![DMN purchasing remittance insurance](/assets/remittance-insurance/dmn-decision-purchasing-insurance.png)
(DMN1.1 decision table for issuing policy)

### Scaling microinsurances (from a technical point of view)

As initally described remittances is mass business which means traffic and many transactions from a technical point of view. Therefore architecture and hosting matters!

The tech11 platform addresses this issue with [cloud services]. This means the platform scales on demand.  
Our recommondation is: use our AWS based cloud services! But in some countries, by local law, the data centeres have to be be in the country where the insurance products are provided.  
Thanks to Kuberentes infrastructure, it's also possible to host the tech11 insurance platform also on-promises (if there is no AWS data center). 

<br><br>

You are interested in more details? Just drop us a <a href="mailto:mail@tech11.com">message</a>


[Wikipedia - Remittance]: https://en.wikipedia.org/wiki/Remittance
[Microinsurance and Remittances]: https://www.cimonline.de/static/media/giz2011-en-microinsurance-remittances.pdf
[tech11 insurance platform]: https://tech11.com/en/products
[cloud services]: https://tech11.com/en/cloud-services
[message]: <address@example.com>
