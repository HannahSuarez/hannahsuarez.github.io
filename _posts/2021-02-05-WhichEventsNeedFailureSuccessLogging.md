---
layout: post
title: "Which Windows auditing events require failure and success logging?"
description: "Use this as a reference to see which ones need failure and success logging"
comments: true
keywords: "security, yaml, elk, elastic, database, servers, blueteam"
---

Which events require failure and success logging? Please see the YAML configuration below and follow the comments.

```
- name: Security
  event.code: 4627, 4703, 4704, 4705, 4720, 4737-4739, 4780-4782, 4793, 4794, 4798, 4799, 5376, 5377

#Account Logon related events
- name: Security
#Success and Failure logging enabled
  event.code: 4774, 4776, 4775, 4776, 4777

#Audit Application Group Management and other
- name: Security
#Success logging enabled
  event.code: 4783-4792

#Audit Computer Account Management
- name: Security
#Success logging enabled
  event.code: 4741-4743

#Audit Distribution Group Management
- name: Security
#Success logging enabled
  event.code: 4749-4753, 4759-4763, 4744-4748

#Audit Security Group Management and Other Accnt Mgmt Events
- name: Security
#Success logging enabled
  event.code: 4782, 4793, 4727-4735, 4737, 4754-4758, 4764, 4799

#Audit User Account Mgmt.
- name: Security
#Success and failure logging enabled
  event.code: 4720, 4722-4726, 4767, 4780, 4781, 4794, 4798, 5376, 5377, 4723, 4766, 4794

#Audit DPAPI Activity
- name: Security
#Success and Failure logging enabled
  event.code: 4692-4685

#Audit PNP Activity
- name: Security
#Success logging enabled
  event.code: 6416, 6419-6424

#Audit process creation and termination. May be noisy.
- name: Security
#Success logging enabled
  event.code: 4688, 4696, 4689

#Audit RPC
- name: Security
#Success logging enabled
  event.code: 5712

#Audit Detailed Directory Service Replication
- name: Security
#Success and Failure logging enabled
  event.code: 4928-4931, 4934-4937

#Audit Directory Access
- name: Security
#Success and Failure logging enabled
  event.code: 4661, 4662

#Audit Directory Service Changes
- name: Security
#Success logging enabled
  event.code: 5136-5139, 5141

#Audit Directory Service Replication
- name: Security
#Success and failure logging enabled
  event.code: 4932, 4933

#Audit group membership
- name: Security
#Success logging enabled
  event.code: 4627

#Audit network policy server
- name: Security
  event.code: 6272-6280

#Audit other logon and logoff events
- name: Security
#Success logging enabled
  event.code: 4649, 4778, 4779, 4964, 4672

#Audit application generated.
- name: Security
  event.code: 4665-4668

#Audit certification services
- name: Security
  event.code: 4868-4898

#Audit certification services
- name: Security
  event.code: 4868-4898

#Audit file share
- name: Security
  #Success and failure logging enabled
  event.code: 5140, 5142-5145, 5168

#Audit file system
- name: Security
  #Success logging enabled
  event.code: 4656, 4658, 4660, 4663, 4664, 4670, 4985, 5051

#Audit file system
- name: Security
  #Success logging enabled
  event.code: 4656, 4658, 4660, 4663, 4664, 4670, 4985, 5051

#Audit filtering platform connection
- name: Security
  #Success and failure logging enabled
  event.code: 5145, 5156, 5158, 5031, 5150, 5151, 5155, 5157, 5159

#Audit handle manipulation
- name: Security
  #Success logging enabled
  event.code: 4658, 4690

#Audit kernel object
- name: Security
  #Success logging enabled
  event.code: 4656, 4658, 4660, 4663

#Audit other object access events
- name: Security
  #Success and failure logging enabled
  event.code: 4671, 4691, 4698, 4699, 4700, 4701, 4702, 5888, 5889, 5890, 5148, 5149

#Audit registry
- name: Security
  #Success logging enabled
  event.code: 4663, 4656, 4658, 4660, 4657, 5039, 4670

#Audit policy change
- name: Security
  #Success logging enabled
  event.code: 4818, 4715, 4719, 4817, 4902, 4904, 4905, 4906, 4908, 4912

#Audit authentication policy chnage
- name: Security
  #Success logging enabled
  event.code: 4670, 4706, 4707, 4713, 4716, 4718, 4739, 4864-4867

#Audit authorization policy change
- name: Security
  #Success logging enabled
  event.code: 4703, 4704, 4705, 4670, 4911, 4913

#Audit MPSSVC rule-level policy change
- name: Security
  #Success and failure logging enabled
  event.code: 4944-4950, 4954, 4956, 4951, 4952, 4953, 4957, 4958

#Audit other policy change events
- name: Security
  #Success and failure logging enabled
  event.code: 4714, 4819, 4826, 4909, 4910, 5063-5070, 5447, 6144, 6145

#Audit priviledge Use
- name: Security
  #Success logging enabled
  event.code: 4673, 4674, 4985

#Audit other system events - windows firewall service, branchcache, key file operation
- name: Security
  #Success and failure logging enabled
  event.code: 5024, 5025, 6400-6409, 4673, 4674, 4985, 5033, 5034, 5058, 5059, 5027-5030, 5032, 5035, 5037

#Audit Security system extension
- name: Security
  #Success logging enabled
  event.code: 4610, 4611, 4614, 4622, 4697

#Audit system integrity
- name: Security
  #Success and failure logging enabled
  event.code: 4612, 4615, 4618, 4816, 5056, 5062, 5061, 5038, 5057, 5060, 6281, 6410

#Audit other events
- name: Security
  #Success logging enabled
  event.code: 1104, 1105, 1108

#Audit Kerberos
- name: Security
  #Success logging enabled
  event.code: 1104, 1105, 1108

#Audit SAM
- name: Security
  #Success logging enabled
  event.code: 1104, 1105, 1108
```

> Note: These are from 2019, so there may have been changes in terms of event ingestion.

> YMMV! Your mileage may vary.
