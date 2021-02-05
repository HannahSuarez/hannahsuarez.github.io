---
layout: post
title: "YAML config for events from the Windows 10 and Windows Server 2016 Security auditing and monitoring reference"
description: "Windows 10 and Windows Server 2016 Security auditing and monitoring reference"
comments: true
keywords: "security, yaml, elk, elastic, database, servers, blueteam"
---

Based on ["Windows 10 and Windows Server 2016 Security auditing and monitoring reference"](https://www.microsoft.com/en-us/download/details.aspx?id=52630).

```
winlogbeat.event_logs:
  - name: Security
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 4627
        - equals.winlog.event_id: 4703
        - equals.winlog.event_id: 4704
        - equals.winlog.event_id: 4705
        - equals.winlog.event_id: 4720
        - equals.winlog.event_id: 4737
        - equals.winlog.event_id: 4738
        - equals.winlog.event_id: 4739
        - equals.winlog.event_id: 4780
        - equals.winlog.event_id: 4781
        - equals.winlog.event_id: 4782
        - equals.winlog.event_id: 4793
        - equals.winlog.event_id: 4794
        - equals.winlog.event_id: 4798
        - equals.winlog.event_id: 4799
        - equals.winlog.event_id: 5376
        - equals.winlog.event_id: 5377
    #Account Logon related events
        - equals.winlog.event_id: 4774
        - equals.winlog.event_id: 4776
        - equals.winlog.event_id: 4775
        - equals.winlog.event_id: 4776
        - equals.winlog.event_id: 4777
    #Audit Application Group Management and other
        - equals.winlog.event_id: 4783
        - equals.winlog.event_id: 4784
        - equals.winlog.event_id: 4785
        - equals.winlog.event_id: 4786
        - equals.winlog.event_id: 4787
        - equals.winlog.event_id: 4788
        - equals.winlog.event_id: 4789
        - equals.winlog.event_id: 4790
        - equals.winlog.event_id: 4783
        - equals.winlog.event_id: 4784
        - equals.winlog.event_id: 4792
        - equals.winlog.event_id: 4791
        - equals.winlog.event_id: 4792
        #Success logging enabled
        - equals.winlog.event_id: 4741
        - equals.winlog.event_id: 4742
        - equals.winlog.event_id: 4743
        #Audit Distribution Group Management
        - equals.winlog.event_id: 4749
        - equals.winlog.event_id: 4750
        - equals.winlog.event_id: 4751
        - equals.winlog.event_id: 4752
        - equals.winlog.event_id: 4753
        - equals.winlog.event_id: 4759
        - equals.winlog.event_id: 4760
        - equals.winlog.event_id: 4761
        - equals.winlog.event_id: 4762
        - equals.winlog.event_id: 4763
        - equals.winlog.event_id: 4744
        - equals.winlog.event_id: 4745
        - equals.winlog.event_id: 4746
        - equals.winlog.event_id: 4747
        - equals.winlog.event_id: 4748
        #Audit Security Group Management and Other Account Management Events
        - equals.winlog.event_id: 4782
        - equals.winlog.event_id: 4793
        - equals.winlog.event_id: 4727
        - equals.winlog.event_id: 4728
        - equals.winlog.event_id: 4729
        - equals.winlog.event_id: 4730
        - equals.winlog.event_id: 4731
        - equals.winlog.event_id: 4732
        - equals.winlog.event_id: 4733
        - equals.winlog.event_id: 4734
        - equals.winlog.event_id: 4735
        - equals.winlog.event_id: 4737
        - equals.winlog.event_id: 4754
        - equals.winlog.event_id: 4755
        - equals.winlog.event_id: 4756
        - equals.winlog.event_id: 4758
        - equals.winlog.event_id: 4764
        - equals.winlog.event_id: 4799
        #Audit User Account Management
        - equals.winlog.event_id: 4720
        - equals.winlog.event_id: 4722
        - equals.winlog.event_id: 4723
        - equals.winlog.event_id: 4724
        - equals.winlog.event_id: 4725
        - equals.winlog.event_id: 4726
        - equals.winlog.event_id: 4767
        - equals.winlog.event_id: 4780
        - equals.winlog.event_id: 4781
        - equals.winlog.event_id: 4794
        - equals.winlog.event_id: 4798
        - equals.winlog.event_id: 5376
        - equals.winlog.event_id: 5377
        - equals.winlog.event_id: 4723
        - equals.winlog.event_id: 4766
        - equals.winlog.event_id: 4794
        #Audit DPAPI Activity
        - equals.winlog.event_id: 4692
        - equals.winlog.event_id: 4693
        - equals.winlog.event_id: 4694
        - equals.winlog.event_id: 4695
        #Audit PNP Activity
        - equals.winlog.event_id: 6416
        - equals.winlog.event_id: 6419
        - equals.winlog.event_id: 6420
        - equals.winlog.event_id: 6421
        - equals.winlog.event_id: 6422
        - equals.winlog.event_id: 6423
        - equals.winlog.event_id: 6424
        #Audit process creation and termination.
        - equals.winlog.event_id: 4688
        - equals.winlog.event_id: 4696
        - equals.winlog.event_id: 4689
        #Audit RPC
        - equals.winlog.event_id: 5712
        #Audit Detailed Directory Service Replication
        - equals.winlog.event_id: 4928
        - equals.winlog.event_id: 4929
        - equals.winlog.event_id: 4930
        - equals.winlog.event_id: 4931
        - equals.winlog.event_id: 4934
        - equals.winlog.event_id: 4935
        - equals.winlog.event_id: 4936
        - equals.winlog.event_id: 4937
        #Audit Directory Access
        - equals.winlog.event_id: 4661
        - equals.winlog.event_id: 4662
        #Audit Directory Service Changes
        - equals.winlog.event_id: 5136
        - equals.winlog.event_id: 5137
        - equals.winlog.event_id: 5138
        - equals.winlog.event_id: 5139
        - equals.winlog.event_id: 5141
        #Audit Directory Service Replication
        - equals.winlog.event_id: 4932
        - equals.winlog.event_id: 4933
        #Audit group membership
        - equals.winlog.event_id: 4627
        #Audit network policy server
        - equals.winlog.event_id: 6272
        - equals.winlog.event_id: 6273
        - equals.winlog.event_id: 6274
        - equals.winlog.event_id: 6275
        - equals.winlog.event_id: 6276
        - equals.winlog.event_id: 6277
        - equals.winlog.event_id: 6278
        - equals.winlog.event_id: 6279
        - equals.winlog.event_id: 6280
        #Audit other logon and logoff events
        - equals.winlog.event_id: 4649
        - equals.winlog.event_id: 4778
        - equals.winlog.event_id: 4779
        - equals.winlog.event_id: 4964
        - equals.winlog.event_id: 4672
        #Audit application generated
        - equals.winlog.event_id: 4665
        - equals.winlog.event_id: 4666
        - equals.winlog.event_id: 4667
        - equals.winlog.event_id: 4668
        #Audit certification services
        - equals.winlog.event_id: 4868
        - equals.winlog.event_id: 4869
        - equals.winlog.event_id: 4870
        - equals.winlog.event_id: 4871
        - equals.winlog.event_id: 4872
        - equals.winlog.event_id: 4873
        - equals.winlog.event_id: 4874
        - equals.winlog.event_id: 4875
        - equals.winlog.event_id: 4876
        - equals.winlog.event_id: 4877
        - equals.winlog.event_id: 4878
        - equals.winlog.event_id: 4879
        - equals.winlog.event_id: 4880
        - equals.winlog.event_id: 4881
        - equals.winlog.event_id: 4882
        - equals.winlog.event_id: 4883
        - equals.winlog.event_id: 4884
        - equals.winlog.event_id: 4885
        - equals.winlog.event_id: 4886
        - equals.winlog.event_id: 4887
        - equals.winlog.event_id: 4888
        - equals.winlog.event_id: 4889
        - equals.winlog.event_id: 4890
        - equals.winlog.event_id: 4891
        - equals.winlog.event_id: 4892
        - equals.winlog.event_id: 4893
        - equals.winlog.event_id: 4894
        - equals.winlog.event_id: 4895
        - equals.winlog.event_id: 4896
        - equals.winlog.event_id: 4897
        - equals.winlog.event_id: 4898
        #Audit file share
        - equals.winlog.event_id: 5140
        - equals.winlog.event_id: 5142
        - equals.winlog.event_id: 5143
        - equals.winlog.event_id: 5144
        - equals.winlog.event_id: 5145
        - equals.winlog.event_id: 5168
        #Audit file system
        - equals.winlog.event_id: 4656
        - equals.winlog.event_id: 4658
        - equals.winlog.event_id: 4660
        - equals.winlog.event_id: 4663
        - equals.winlog.event_id: 4664
        - equals.winlog.event_id: 4670
        - equals.winlog.event_id: 4985
        - equals.winlog.event_id: 5051
        #Audit filtering platform connection
        - equals.winlog.event_id: 5145
        - equals.winlog.event_id: 5156
        - equals.winlog.event_id: 5158
        - equals.winlog.event_id: 5031
        - equals.winlog.event_id: 5150
        - equals.winlog.event_id: 5151
        - equals.winlog.event_id: 5155
        - equals.winlog.event_id: 5157
        - equals.winlog.event_id: 5159
        #Audit handle manipulation
        - equals.winlog.event_id: 4658
        - equals.winlog.event_id: 4690
        #Audit kernel object
        - equals.winlog.event_id: 4656
        - equals.winlog.event_id: 4658
        - equals.winlog.event_id: 4660
        - equals.winlog.event_id: 4663
          #Audit other object access events
        - equals.winlog.event_id: 4671
        - equals.winlog.event_id: 4691
        - equals.winlog.event_id: 4698
        - equals.winlog.event_id: 4699
        - equals.winlog.event_id: 4700
        - equals.winlog.event_id: 4701
        - equals.winlog.event_id: 4702
        - equals.winlog.event_id: 5888
        - equals.winlog.event_id: 5889
        - equals.winlog.event_id: 5890
        - equals.winlog.event_id: 5148
        - equals.winlog.event_id: 5149
        #Audit registry
        - equals.winlog.event_id: 4663
        - equals.winlog.event_id: 4656
        - equals.winlog.event_id: 4658
        - equals.winlog.event_id: 4660
        - equals.winlog.event_id: 4657
        - equals.winlog.event_id: 5039
        - equals.winlog.event_id: 4670
        #Audit policy change
        - equals.winlog.event_id: 4818
        - equals.winlog.event_id: 4715
        - equals.winlog.event_id: 4719
        - equals.winlog.event_id: 4817
        - equals.winlog.event_id: 4902
        - equals.winlog.event_id: 4904
        - equals.winlog.event_id: 4905
        - equals.winlog.event_id: 4906
        - equals.winlog.event_id: 4908
        - equals.winlog.event_id: 4912
        #Audit authentication policy change
        - equals.winlog.event_id: 4670
        - equals.winlog.event_id: 4706
        - equals.winlog.event_id: 4707
        - equals.winlog.event_id: 4713
        - equals.winlog.event_id: 4716
        - equals.winlog.event_id: 4718
        - equals.winlog.event_id: 4739
        - equals.winlog.event_id: 4864
        - equals.winlog.event_id: 4865
        - equals.winlog.event_id: 4866
        - equals.winlog.event_id: 4867
        #Audit Kerberos
        - equals.winlog.event_id: 4768
        - equals.winlog.event_id: 4771
        - equals.winlog.event_id: 4772
        #Audit authorization policy change
        - equals.winlog.event_id: 4703
        - equals.winlog.event_id: 4704
        - equals.winlog.event_id: 4705
        - equals.winlog.event_id: 4670
        - equals.winlog.event_id: 4911
        - equals.winlog.event_id: 4913
        #Audit MPSSVC rule-level policy change
        - equals.winlog.event_id: 4944
        - equals.winlog.event_id: 4945
        - equals.winlog.event_id: 4946
        - equals.winlog.event_id: 4947
        - equals.winlog.event_id: 4948
        - equals.winlog.event_id: 4949
        - equals.winlog.event_id: 4950
        - equals.winlog.event_id: 4954
        - equals.winlog.event_id: 4956
        - equals.winlog.event_id: 4951
        - equals.winlog.event_id: 4952
        - equals.winlog.event_id: 4953
        - equals.winlog.event_id: 4957
        - equals.winlog.event_id: 4958
        #Audit other policy change events
        - equals.winlog.event_id: 4714
        - equals.winlog.event_id: 4819
        - equals.winlog.event_id: 4826
        - equals.winlog.event_id: 4909
        - equals.winlog.event_id: 4910
        - equals.winlog.event_id: 5063
        - equals.winlog.event_id: 5064
        - equals.winlog.event_id: 5065
        - equals.winlog.event_id: 5066
        - equals.winlog.event_id: 5067
        - equals.winlog.event_id: 5068
        - equals.winlog.event_id: 5069
        - equals.winlog.event_id: 5070
        - equals.winlog.event_id: 5447
        - equals.winlog.event_id: 6144
        - equals.winlog.event_id: 6145
        #Audit priviledge Use
        - equals.winlog.event_id: 4673
        - equals.winlog.event_id: 4674
        - equals.winlog.event_id: 4985
        #Audit other system events - Windows Firewall service, branchcache, key file operation
        - equals.winlog.event_id: 5024
        - equals.winlog.event_id: 5025
        - equals.winlog.event_id: 6400
        - equals.winlog.event_id: 6401
        - equals.winlog.event_id: 6402
        - equals.winlog.event_id: 6403
        - equals.winlog.event_id: 6404
        - equals.winlog.event_id: 6405
        - equals.winlog.event_id: 6406
        - equals.winlog.event_id: 6407
        - equals.winlog.event_id: 6408
        - equals.winlog.event_id: 6409
        - equals.winlog.event_id: 4673
        - equals.winlog.event_id: 4674
        - equals.winlog.event_id: 4985
        - equals.winlog.event_id: 5033
        - equals.winlog.event_id: 5034
        - equals.winlog.event_id: 5058
        - equals.winlog.event_id: 5059
        - equals.winlog.event_id: 5027
        - equals.winlog.event_id: 5028
        - equals.winlog.event_id: 5029
        - equals.winlog.event_id: 5030
        - equals.winlog.event_id: 5032
        - equals.winlog.event_id: 5035
        - equals.winlog.event_id: 5037
        #Audit Security system extension
        - equals.winlog.event_id: 4610
        - equals.winlog.event_id: 4611
        - equals.winlog.event_id: 4614
        - equals.winlog.event_id: 4622
        - equals.winlog.event_id: 4697
        #Audit system integrity
        - equals.winlog.event_id: 4612
        - equals.winlog.event_id: 4615
        - equals.winlog.event_id: 4618
        - equals.winlog.event_id: 4816
        - equals.winlog.event_id: 5056
        - equals.winlog.event_id: 5062
        - equals.winlog.event_id: 5061
        - equals.winlog.event_id: 5038
        - equals.winlog.event_id: 5057
        - equals.winlog.event_id: 5060
        - equals.winlog.event_id: 6281
        - equals.winlog.event_id: 6410
        #Audit other log related events
        - equals.winlog.event_id: 1102
        - equals.winlog.event_id: 1104
        - equals.winlog.event_id: 1105
        - equals.winlog.event_id: 1108
        #Audit SAM
        - equals.winlog.event_id: 4661
```

> YMMV! Your mileage may vary.
