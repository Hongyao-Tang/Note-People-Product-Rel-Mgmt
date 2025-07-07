---
author: "Hongyao Tang"
title: "Business"
date: "2025-07-06"
tags: [
    "product",
]
ShowToc: true
weight: 2
---

# Customer
## App Engineer - powerful to use

## IT Engineer - easy to use, and worry-free
It’s not just about fast chips - it’s about delivering a balanced, usable system.
NVL72 was co-designed with data center infrastructure in mind. 
- NVIDIA worked on the compute architecture in tandem with system engineers who figured out power delivery and cooling
- and in tandem with facility engineers who specified how to install and run these things. 


### S - Diffucult deployment and large scale
- NVL72 is such a complex system
  - individually cable 72 GPUs with NVLink

T - DGX turnkey solition/Pre-Integrated Rack Appliance
- comes assembled with all 18 compute nodes, all 9 NVSwitch units, internal NVLink cabling, power distribution, and a cooling system. 
- rack also includes
  - NVIDIA Base Command Manager cluster-management software and
  - SLURM and Kubernetes for cluster-job scheduling and orchestration.

R

Out-of-the-box
- One simply connects the rack to facility power, hooks up the water cooling interfaces, connects the InfiniBand cables to your network, and turns it on!
- ensures that the system is built correctly and validated by NVIDIA and thus accelerates deployment 

Multi-rack deployments are called AI factories where the racks are the production lines for AI models


### S - Power
- NVL72 rack is incredibly high compute dense计算密度高
- means it draws a very high amount of power for a single rack. high power density
- A mini power substation. A fully loaded NVL72 can consume up to about 120 kW of power under max load.
  - Each compute node in the NVL72 contains 2 Grace-Blackwell superships which together consume on the order of 5-6 kW. 
  - With 18 compute nodes, the total power consumed is about 100 kW. 
  - The NVSwitch trays, network switches, and cooling pumps account for approximately 20 kW

T - dedicated power distribution units (PDUs) and careful monitoring

<u>Multiple high-capacity circuits</u> 
- Data centers can’t just use a single standard power feed
- typically provision multiple high-capacity circuits to feed this kind of power
  - push two separate power feeds into the rack for redundancy where each feed is capable of 60 kW
  - Within the rack,
    - power is distributed to the power supplies of each 1U compute node. 
    - The power is converted from AC to DC for the local electronics. 


<u>Avoid spike</u>
- capacitors or sequencing to avoid power transients 功率瞬变
  - ramping from idle to full power, could rapidly draw tens of kW of power in just milliseconds.
  - large voltage drops.
- The system might stagger the GPU boost clocks by tiny intervals, 
  - so they don’t all spike at exactly the same microsecond, smoothing out the surge. 


R

Redundancy
- Under normal operation, the load is balanced between the feeds. 
- And if one feed fails, the system could shed some load or throttle the GPUs to stay within the remaining feed’s capacity. This kind of redundancy is important 
- to protect against a blown circuit halting your multi-month training job.

High ROI
- although 120 kW is a lot in one rack, you are also getting a lot of work done per watt than  several racks of older equipment,



### S - 120 kW in one rack need cooling
- Air Cooling would require hurricane-like airflow and would be extremely loud and inefficient 

T - fully liquid-cooled system
- Each Grace-Blackwell superchip module and each NVSwitch chip has a cold plate attached.
  - A cold plate is a metal plate with internal tubing that sits directly on the component.
- All these cold plates are linked by hoses, manifolds, and pumps
- A water-based coolant liquid flows through the tubing to carry away heat. 
- heat exchanger
  - The rack then has supply and return connections to the external facility’s chilled water system. 
  - Often, there’s a heat exchanger called a Cooling Distribution Unit (CDU) either built into the rack or immediately next to it. The CDU transfers heat from the rack’s internal coolant loop to the data center’s water loop.
- Cooling tower
  - The facility provides chilled water at 20-30°C.
  - The water absorbs the heat through the heat exchanger. 
  - The warmed-up water is then pumped back into the chillers or cooling towers to be cooled again. 
- In modern designs, they might even run warm water cooling in which 
  - chilled water comes into the system at 30°C and leaves at 45°C. 
  - The water can then be cooled by evaporative cooling towers without active refrigeration which improves overall efficiency.

<u>rack have quick-disconnect couplings for each node</u>
- slide a server in or out without spilling the coolant

R

coolant flow rate has to be sufficient to remove that heat quickly.
- 10+ liters per minute of water flowing through the system to dissipate 120 kW of power with a reasonable temperature increase

effective
- liquid coolant, can carry far more heat per unit of flow than air
- so liquid cooling is vastly more effective when running at high watts in small spaces.

running chips cooler 
- improves reliability and even efficiency since power leakage is lower when running at lower temperatures.
- The NVL72 keeps GPU temps in the 50-70°C range. reduces thermal GPU throttling. The GPUs can sustain their maximum clocks without hitting temperature limits.

easy to use
- The NVL72 rack, with its built-in internal liquid cooling, can be connected directly to the cooling loop.

Side effect附带缺点
- weight of the rack
  - 3000 lbs (1.3–1.4 metric tons) roughly the weight of a small car, when filled with hardware and coolant.
- Data centers with raised floors have to check that the floor can support this load measured in pounds per square foot. reinforced slabs or supported by additional struts
- Moving such a rack requires special equipment such as forklifts.








## Finance and purchase - ROI
-  Worthy? if it’s worth investing in this bleeding-edge hardware


### S - [Investment] HW depreciation, cost from financial POV
-企业在购置资产时通常一次性支付全部费用
- 资产价值消耗的客观性
  - 无形资产（如专利、软件）虽无物理损耗，但存在法律保护期或技术替代风险。例如，一项专利权有效期10年，其价值需在10年内逐步释放。
  - 固定资产（如设备、房屋）会因物理磨损、技术过时或使用年限缩短价值。
- 财务波动
  - 例如，一台价值100万元的机器预计使用5年，若一次性计入首年成本，将导致利润异常波动（首年巨亏，后4年虚增利润）
  - 一次性计入成本会导致利润大幅波动，不利于投资者决策。例如，航空公司购买一架飞机需数亿元，若不计提折旧，首年财报将严重失真。

T - 将“一次性支出”转化为“持续成本”，实现收入与成本的配比
企业在购置资产时通常一次性支付全部费用，但会计和财务管理要求将资产成本在其有效使用期内合理分摊，以更准确地反映资产对各期经营成果的贡献。
- 摊销amortization - 无形资产（专利、商标、软件）；长期待摊费用（开办费、装修费）
- 折旧depreciation -固定资产（设备、房屋、车辆） 

R
- 真实反映资产价值
- 平滑利润，避免财务波动
- 财报准确有利于投资者




### S - ROI/performance per dollar including hardware deprecation and power

R

fewer total GPUs for the same work.
- a hundred H100 GPUs = 50 Blackwell GPUs re. throughput for the same work
- even if each Blackwell costs more than an H100, buying half as many could be cost-neutral or better.
- one hundred H100s might draw 70 kW whereas fifty Blackwells might draw 50 kW
- fewer GPUs means fewer servers to maintain, which means less overhead in CPUs, RAM, and networking for those servers provides even further savings. 

a single powerful system instead of many smaller ones can 
- simplify your system architecture
- This simplification improves operational efficiency by lowering power consumption and reducing network complexity.

All told, an upgrade to new hardware can pay for itself in 1–2 years in some cases, if you have enough workload to keep it busy.




### S - [Return] Get most out of the hardware
- machine is powerful and expensive
  - a system like NVL72 is a multi-million dollar asset, and it could consume tens of thousands of dollars in electricity per month. 
- make sure you’re getting the most out of it.
- make every flop and every byte count.使每个翻位和每个字节计数。

- ensures that people value the resource

T - monitoring utilization over time

Nvidia DCGM (Data Center GPU Manager)
- can track metrics on each GPU for things like GPU utilization %, memory usage, temperature, and NVLink throughput.

T2 - internal teams use their own budget to pay per GPU-hour of usage.


R
Operating an NVL72 effectively
- GPUs Utilization: to be near 100%
  - a data loading bottleneck
  - a synchronization issue
- NVLink Utilization: not saturating
  - communication is likely the culprit
- BlueField DPUs and NICs: not saturating your storage links when reading data
- power draw per node or per GPU
  - might cap the power or clocks of GPUs if full performance isn’t needed, to save energy and cost
  - Higher clock speeds generally mean more power is consumed, and GPUs can dynamically adjust their clock speeds to manage power/energy and temperature and cost

- 72 GPU-hours which might cost hundreds of dollars worth of electricity and amortized hardware cost.


# Partner
## Manufacturing
### 生产合作模式
<u>S - 产品设计研发能力不足，生产制造能力不足</u>
- 企业希望拓展新市场或进入新领域，但缺乏相关产品的设计和生产经验。

T - 用制造商设计方案和生产

ODM：**B设计，B生产**，A品牌，A销售==俗称“贴牌”，就是工厂的产品，别人的品牌
- A品牌方，销售渠道方
- B设计生产制造方，ODM方
- ODM模式允许品牌方直接采用制造商的设计方案，或在其基础上进行修改(定制)

A

例如，美的家电品牌通过ODM模式快速推出新款产品

R
- 缩短研发周期，降低研发成本。
- 快速推出具有市场竞争力的产品。
- 一些初创企业通过ODM模式快速推出产品，验证市场可行性后再逐步投入自主研发。


<u> S - 生产能力不足或成本过高的问题</u>
- 企业资源有限，难以同时兼顾研发、设计、生产和销售等全链条环节。
- 许多品牌方拥有核心技术和设计能力，但缺乏自建工厂或高效生产能力，导致产能受限或生产成本过高。

T - 找代工/OEM

A设计，B生产，A品牌，A销售==代工，代生产，别人的技术和品牌，工厂只生产
- A品牌方
- B生产制造方，OEM方
- OEM模式允许品牌方将生产环节外包给专业制造商，利用其成熟的工艺、设备和规模效应

A

例如，苹果公司将iPhone的生产委托给富士康

R
- 快速扩大产能
- 保证了产品质量

- 又避免了高额的固定资产投资
- 并降低生产成本

- 企业需要快速推出新产品以抢占市场先机，但自建生产线周期长、风险高

<u>S - 全部自己</u>
T

OBM：A设计，A生产，A品牌，A销售==全部自己，工厂自己设计自产自销



A
|Component|Partner|
|-|-|
|servers and racks|Supermicro/HPE|
|Blackwell GPU| TSMC 4 nm process|
|Blackwell Ultra HBM3E |	SK 海力士预计将独家供应英伟达  <br> 三星这边，HBM3E此前一直未能获得英伟达品质认证，而最新消息则是三星新 HBM3E 在日前英伟达的审核中获得令人满意的评分，预计最快 6 月初通过英伟达等的品质认证|



## Solution & Sales
### 销售渠道模式
first-party sale - the primary vendor selling and supporting it
- Microsoft Azure Local - Microsoft itself

third-party vendors - offer solutions  to provide pre-configured, tightly integrated infrastructure, often including hardware like servers and networking components, along with software and support. 
- Microsoft recommends purchasing Premier Solutions from these partners for the best experience. 
- Microsoft Azure Local -  Dell AX


A
Hewlett Packard Enterprise (HPE)
- Shipped their first NVIDIA Blackwell family-based solution

CoreWeave
- NVIDIA envisions offering a rack as-a-service through its partners so companies can rent a slice of a supercomputer rather than building everything themselves. 
- First cloud provider to make NVIDIA GB200 NVL72-based instances generally available


# Roadmap of HW
### S - How to deliver the future
T - Doubling something every generation for every year 

<u>GPU naming after scientists</u>
- Blackwell GPU
- Rubin GPU
- Feynmann GPU

|(G,V)|(B,R,F)|(2,3)|200||
|-|-|-|-|-|
|CPU|GPU|Ultra|Constant|Year|
||B|2|00|2024|
|G|B|2|00|
||B|3|00|2025|
|G|B|3|00|
||R|2|00|2026|
|V|R|2|00|
||R|3|00|2027|
|V|R|3|00|
||F|2|00|2028|


<u>Strtegy: Doubling something every generation for every year</u>
- One year(2025 B300/GB300) they double memory per GPU( 192 GB → 288 GB)
- Another year(2026, R200/VR200) they double interconnect/NVLink bandwidth/throughput (900 GB/s → 1.8 TB/s)
- Another year(2027 R300/VR300) they double the number of dies (2 dies → 4 dies )
- Over a few years, the compound effect of this doubling is huge.


A
|Year|Generation|Process node|Computing|Memory|Network|Others|Use case|
|-|-|-|-|-|-|-|-|
|2024|Blackwell (B200) and Grace-Blackwell superchip (GB200)|4nm|2-die|192 GB per GPU|-|introduce usage of FP4 precision||
|2025|Blackwell Ultra (B300) and Grace-Blackwell Ultra superchip (GB300)|4nm|2-die|**increase memory from 192 GB to 288 GB per GPU**|-|generous usage of FP4 precision|real-time AI agents and multi-modal models that demand maximum throughput|
|2026|Rubin GPU (R200) and Vera-Rubin Supership (VR200)|TSMC’s 3nm |   increase SM counts significantly to around 200 SMs per die. This is up from 140-ish in Blackwell. |HBM4 with LPDDR6|**NVLink 6**|speculation on second-generation FP4 or even experimental 2-bit precisions |
|2027|Rubin Ultra (R300) and Vera-Rubin Ultra(VR300)|-|**from 2 to 4-die**|16 HBM stacks totaling 1 TB of HBM memory|
|2028|Feynmann GPU|2nm TSMC process|**double the number of dies from 4 to 8**|-|-|-|Reasoning requires a lot more inference-time computation than previous, non-reasoning models|
