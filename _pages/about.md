---
permalink: /
title:
excerpt: "About me"
author_profile: true
redirect_from:
  - /about/
  - /about.html
---


I am a third-year PhD student in [Population Health](https://pophealth.wisc.edu/degree-programs/about-the-programs/population-health/) at [University of Wisconsin-Madison](https://www.wisc.edu/). My advisor is Dr. [Maureen Smith](https://pophealth.wisc.edu/staff/smith-maureen/). I explore the association between telehealth use and unplanned events during COVID-19 and multilevel factors that may improve colorectal cancer screening rates at rural and urban clinics in Wisconsin, by working closely with Dr. [Jessica Cao](https://pophealth.wisc.edu/staff/cao-jessica-ying/), Dr. [Jennifer Weiss](https://www.medicine.wisc.edu/people-search/people/staff/565/Weiss_Jennifer), and Dr. [Guanhua Chen](https://biostat.wiscweb.wisc.edu/staff/chen-guanhua/).

I was trained in computer vision, machine learning and natural language processing. I got my master's degrees in Biomedical Data Science and Computer Science from [University of Wisconsin-Madison](https://biostat.wiscweb.wisc.edu/) and [University of Connecticut](https://www.cse.uconn.edu/), respectively. I received my bachelor's degree in Electrical Engineering and Computer Science from [Southeast University](https://www.seu.edu.cn/english/).

I am interested in trustworthy machine learning in healthcare. I would like to know if causal inference can help better understand machine learning models when focusing on health services research and clinical problems. With causal inference embedded, these black-box models may become more interpretable and generalizable, rather than being limited to finding patterns in the data.


Stat 888
------
Telehealth has been gradually equipped to the U.S. healthcare system in the past few decades [1], while we noticed that COVID-19 has triggered rapid expansion of telehealth [2-3] to help maintain social distancing to reduce the risk of infection. In February 2020, the Centers for Disease Control and Prevention (CDC) issued guidance advising individuals and healthcare providers in areas affected by the COVID-19 pandemic to practice social distancing practices, specifically recommending that healthcare facilities and providers offer clinical services virtually such as telehealth. In March 2020, Centers for Medicare & Medicaid Services (CMS) announced initial telehealth flexibilities for Medicare beneficiaries, allowing the same payment level for telehealth as for in-person visits. [4]

However, there is limited evidence about the effects of telehealth on long-term patient outcomes. [5-6] Some people support telehealth due to its timely care access [7-8], while some aruge that telehealth is not an adequate substitute for in-person visits, which can cause even more delayed or missed care, resulting in worse outcomes. [9-10] Uncertainty and debates have prevented the policymakers, insurers, healthcare providers and other entities to make permanent decisions on telehealth in the post-pandemic future. [11-13]

This formally raises the question: compared to in-person visits, are telehealth visits beneficial in improving patient outcomes, such as fewer hospitalizations?


**Model the Problem**

In order to simplify the problem, three random variables are defined.
- Treatment effect $$A \in \{0, 1\}$$, where $$A = 1$$ for telehealth visit and $$A = 0$$ for in-person visit.
- Outcome $$Y \in N^0$$, a non-negative integer, indicating the number of hospitalizations within 30 days of the visit.
- Patient characteristics $$X \in R^d$$, a $$d$$ real-valued vector, which including patients' sociodemographics and health conditions at baseline. 

Sociodemographics contain age group (65-74 years old, 75-85, and 86+), gender (female/non-female), race/ethnicity(non-hispanic white/other), Medicaid enrollment (binary indicator), disability entitlement (binary indicator) and geographical residence (urban, suburban, large town, small town/isolated rural). The hierarchical condition categories (HCC) score and a binary indicator of having three or more chronic conditions serve as the description of patients' health conditions.


**Causal Effect**

There is an underlying assumption to this question: sampled participants in the study are able to access telehealth services. However, telehealth is not available to everyone, such as those who do not have access to the Internet. Therefore, it is reasonable to define population average treatment effects $$E[Y(A = 1) - Y(A = 0) \mid S = 1]$$ for this problem, where $$S \in \{0, 1\}$$ with $$S = 1$$ represents being sampled in this study.


**Hypotheses**

Ideally, the directed acyclic graph (DAG) can be as simple as $$A \rightarrow Y \leftarrow X$$ since $$X$$ precedes $$A$$ and $$A$$ precedes $$Y$$, which indicates both $$X$$ and $$A$$ can affect $$Y$$ but pre-existing characteristics $$X$$ and the treatment $$A$$ cannot be affected by $$Y$$. This also assumes that individuals receiving treatment $$(A = 1)$$ or not $$(A = 0)$$ are expected to be exchangeable, i.e., $$Y(a) \| A $$ for $$a \in \{0, 1\}$$.

However, confounding variables such as patients' demographics and preferences on telehealth vs in-person services, as well as their pre-existing health conditions, may affect their treatment $$A$$. Then it adds a path from $$X$$ to $$A$$, implying that there will be two paths from $$X$$ to $$Y$$ in a single DAG: $$X \rightarrow A \rightarrow Y$$ and $$X \rightarrow Y$$ if assuming confounding variables are observed. Furthermore, if taking unobserved characteristics $$U \subseteq X$$ into consideration as well, then the DAG can contain two paths from $$U$$ to $$Y$$: $$U \rightarrow A \rightarrow Y$$ and $$U \rightarrow C \rightarrow Y$$ where the union of observed characteristics $$C \subseteq X$$ and unobserved characteristics $$U$$ is the characteristics $$X$$. In other words, the effect of unobserved variables on the outcomes will be passed through to the observed variables.







**Reference**

[1] Jagarapu, Jawahar, and Rashmin C. Savani. "A brief history of telemedicine and the evolution of teleneonatology." In Seminars in Perinatology, vol. 45, no. 5, p. 151416. WB Saunders, 2021.

[2] [https://www.cdc.gov/mmwr/volumes/69/wr/mm6943a3.htm](https://www.cdc.gov/mmwr/volumes/69/wr/mm6943a3.htm)

[3] [https://aspe.hhs.gov/sites/default/files/documents/a1d5d810fe3433e18b192be42dbf2351/medicare-telehealth-report.pdf](https://aspe.hhs.gov/sites/default/files/documents/a1d5d810fe3433e18b192be42dbf2351/medicare-telehealth-report.pdf)

[4] [https://www.medicare.gov/coverage/telehealth](https://www.medicare.gov/coverage/telehealth)

[5] Goldberg, Elizabeth M., Frances N. Jiménez, Kevin Chen, Natalie M. Davoodi, Melinda Li, Daniel H. Strauss, Maria Zou, Kate Guthrie, and Roland C. Merchant. "Telehealth was beneficial during COVID‐19 for older Americans: a qualitative study with physicians." Journal of the American Geriatrics Society 69, no. 11 (2021): 3034-3043.

[6] [https://www.healthaffairs.org/do/10.1377/forefront.20211019.985495/](https://www.healthaffairs.org/do/10.1377/forefront.20211019.985495/)

[7] Johnson, Pamela Jo, Neha Ghildayal, Andrew C. Ward, Bjorn C. Westgard, Lori L. Boland, and Jon S. Hokanson. "Disparities in potentially avoidable emergency department (ED) care: ED visits for ambulatory care sensitive conditions." Medical care (2012): 1020-1028.

[8] Lee, Ivy, Carrie Kovarik, Trilokraj Tejasvi, Michelle Pizarro, and Jules B. Lipoff. "Telehealth: Helping your patients and practice survive and thrive during the COVID-19 crisis with rapid quality implementation." Journal of the American Academy of Dermatology 82, no. 5 (2020): 1213-1214.

[9] Bavafa, Hessam, Lorin M. Hitt, and Christian Terwiesch. "The impact of e-visits on visit frequencies and patient health: Evidence from primary care." Management Science 64, no. 12 (2018): 5461-5480.

[10] Li, Kathleen Y., Sophia Ng, Ziwei Zhu, Jeffrey S. McCullough, Keith E. Kocher, and Chad Ellimoottil. "Association Between Primary Care Practice Telehealth Use and Acute Care Visits for Ambulatory Care–Sensitive Conditions During COVID-19." JAMA network open 5, no. 3 (2022): e225484-e225484.

[11] [https://www.commonwealthfund.org/publications/issue-briefs/2021/jun/states-actions-expand-telemedicine-access-covid-19](https://www.commonwealthfund.org/publications/issue-briefs/2021/jun/states-actions-expand-telemedicine-access-covid-19)

[12] Shachar, Carmel, Jaclyn Engel, and Glyn Elwyn. "Implications for telehealth in a postpandemic future: regulatory and privacy issues." Jama 323, no. 23 (2020): 2375-2376.

[13] Bashshur, Rashid L., Charles R. Doarn, Julio M. Frenk, Joseph C. Kvedar, Gary W. Shannon, and James O. Woolliscroft. "Beyond the COVID pandemic, telemedicine, and health care." Telemedicine and e-Health 26, no. 11 (2020): 1310-1313.