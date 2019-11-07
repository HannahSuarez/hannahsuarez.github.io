---
layout: post
title: "Business Continuity Planning"
description: "High level overview on business continuity planning"
comments: true
keywords: "it, planning, risk management, business continuity"
---

This is an article written for a secure file transfer product.

[Original article here](https://www.sftpplus.com/articles/2018/sftpplus-business-continuity-article.html)

---

# Full content below

## Introduction

**What is business continuity planning (BCP)?**

According to `Wikipedia <https://en.wikipedia.org/wiki/Business_continuity_planning>`_, business continuity planning is the process of creating systems of prevention and recovery to deal with potential threats to a company.

Business Continuity Planning also includes these five components as defined by the `SANS Institute <https://en.wikipedia.org/wiki/Disaster_recovery_plan#Relationship_to_the_Business_Continuity_Plan>`_.
These components are:

* Business Resumption Plan
* Occupant Emergency Plan
* Continuity of Operations Plan
* Incident Management Plan
* Disaster Recovery Plan (DRP)

We have decided to provide a high level overview for this article.
While secure file transfer is just a component of business continuity planning, it is still an important component of it.
We hope that after reading this post, that you also recognize secure file transfers to be part of the Business Continuity Planning process.


## Assigning risk ratings

Planning involves conducting a risk assessment of your organization.
In this case, planning involves determining what is considered IT risk versus Business risk.

By conducting a risk analysis, you can identify portions of your business resources, identify known risks to these business resources, and assign a risk rating.

According to the `Cisco Systems Network Security Policy Best Practices White Paper <https://www.cisco.com/c/en/us/support/docs/availability/high-availability/13601-secpol.html>`_, the following are rating guidelines based on a three-tier risk level.
These are examples from purely a network security level and there are other models and guidelines
available that cover a more generalized approach.

The following are excerpts from the above whitepaper:


**Low Risk**

These are *systems or data that if compromised (data viewed by unauthorized personnel, data corrupted, or data lost) would not disrupt the business or cause legal or financial ramifications. The targeted system or data can be easily restored and does not permit further access of other systems.*


**Medium Risk**

These are *systems or data that if compromised (data viewed by unauthorized personnel, data corrupted, or data lost) would cause a moderate disruption in the business, minor legal or financial ramifications, or provide further access to other systems. The targeted system or data requires a moderate effort to restore or the restoration process is disruptive to the system.*


**High Risk**

These are *systems or data that if compromised (data viewed by unauthorized personnel, data corrupted, or data lost) would cause an extreme disruption in the business, cause major legal or financial ramifications, or threaten the health and safety of a person. The targeted system or data requires significant effort to restore or the restoration process is disruptive to the business or other systems.*

From the perspective of secure file transfer, you will need to consider at which level your assets (such as the assets covered in the scope of file transfers) fall under which of these risk categories.


## Establishing a business continuity structure / policy

Part of the planning process also involves establishing a business continuity structure.

Having a business continuity policy will require building a team and a governance structure around it.
Within the policy, ensure to outline the roles and responsibilities of those that are going to be impacted by this document.

Within the context of secure file transfers, the policy could outline the role of the secure file transfer administrator and to make aware that it is their responsibility to ensure successful Continuity of Operations.
In this example, the same administrator could also be the support or testing lead to ensure that the failover file transfer system is tested and verified should there be an issue with the main server.

On that note, for those interested in more details about how SFTPPlus can help administrators meet Continuity of Operations demands, please `read our introduction to SFTPPlus and high availability or resiliency environments <https://www.sftpplus.com/articles/2018/sftpplus-ha-resiliency-intro>`_.

In conclusion, the business continuity policy should ensure that the organization has been provided a general understanding of the policy, purpose, guidelines and definitions around the business continuity plan.


## Incident Management and Incident Response

Part of business continuity planning is around incident management and incident response.

What is the relationship between Business Continuity Planning and Incident Management Plan? 
According to `NIST Security Incident Handling guide <https://nvlpubs.nist.gov/nistpubs/specialpublications/nist.sp.800-61r2.pdf>`_ (the National Institute of Standards and Technology), *“organizations should ensure that incident response policies and procedures and business continuity processes are in sync. Computer security incidents undermine the business resilience of an organization. Business continuity planning professionals should be made aware of incidents and their impacts so they can fine-tune business impact assessments, risk assessments, and continuity of operations plans.”*

Within the context of secure file transfers, SFTPPlus emits an audit trail for administrators to monitor events and for audit assurance purposes, which can help assist in incident management and response.
For further readings about procedures, we recommend the `NIST Security Incident Handling guide <https://nvlpubs.nist.gov/nistpubs/specialpublications/nist.sp.800-61r2.pdf>`_.
Our documentation on the audit trail also provides a useful starting point on how you can administer SFTPPlus to be compliant to your auditing needs.


## Implementation

Implementation is the practice stage.
The importance of implementation is the prevention of business risk.

The recovery point objective (RPO) and recovery time objective (RTO) are baseline data that administrators should be aware of when implementing the business continuity plan.

For example, a secure file transfer administrator can ask themselves questions such as *"What is the recovery time actual (RTA) in contrast to the recovery time objective (RTO) for the file transfer application during an actual disaster or exercise?"*

The Business Impact Analysis should uncover which systems are mission critical and non-critical, which can further impact the RPO and RTO, as an example.
In this example, you may need to ensure an active-active high availability setup is in place with the backup server in the cloud rather than on-premise.
In this scenario, you may be targeting 100% Recovery Consistency Objective (RCO) for a business process.


## Exercise / Testing / Action

Part of business continuity plan should include a review process to modify the existing policy.
This process should be able to adapt to lessons learned - either from an actual disaster event or from an exercise.

The review process ensures that the policy, posture and practices are being re-evaluated accordingly. 

The Business Continuity Plan should end up being a dynamic document that can adapt to the constantly changing business and IT environment and needs.
This dynamic should also include education and evaluation of staff skills involved. 


## ISO guidelines for further reading 

Continual improvement with your business continuity plan are also covered by guidelines such as `ISO 22301 <https://www.iso.org/standard/50038.html>`_ "Societal security -- Business continuity management systems --- Requirements". This guide *“specifies requirements to plan, establish, implement, operate, monitor, review, maintain and continually improve a documented management system to protect against, reduce the likelihood of occurrence, prepare for, respond to, and recover from disruptive incidents when they arise.”*

And for those focusing on the information security management system, the ISO/IEC 27001:2013
`standard <https://www.iso.org/standard/54534.html>`_ *“specifies the requirements for establishing, implementing, maintaining and continually improving an information security management system within the context of the organization. It also includes requirements for the assessment and treatment of information security risks tailored to the needs of the organization.”*
