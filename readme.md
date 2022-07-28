## [What is Apache Kafka?](https://www.youtube.com/watch?v=FKgi3n-FyNU) (quick)

Databases encourage us to think in terms of **things in the world with state**

This worked for decades

But we’re now starting to think in terms of **events**

Events are indications in time that a thing took place

Instead of a database for events, we use logs

A log is an ordered sequence of events

- They are easy to reason about
- They scale well

Kafka is a system for managing these logs

We call these logs **topics**

A topic is an ordered collection of events stored in a durable way (on disk, replicated)

Topics store data for various periods of time (minutes/hours/days/years/forever)

Topics can be small, or enormous 

**Each event is a thing happening in the business**

- A user updates their shipping address
- A thermostat reports temperature increase
- A Ship unloads cargo
- Etc...

Systems used to be **monolithic** ==> but they got too big and complex for programmers

Now we write lots of small programs (microservices) which can talk to each other through :drum: … kafka topics!

Instead of running cumbersome batch processes, we can perform actions (with services) as close to immediate as possible - e.g. in real-time analytics

So far we have: **events, topics, services, real-time analytics**

We also have **Kafka Connect** to help interface with other (legacy) systems (DBs, other products that are not kafka)

KC gets the data into the topic and back out into the DB

It does grouping, aggregating, filtering, enrichment (joins in DB)

Kafka Streams handles the framework and infrastructure to get all that done

## [**Apache Kafka Fundamentals Playlist**](https://www.youtube.com/watch?v=-DyWhcX3Dpc&list=PLa7VYi0yPIH2PelhRHoFR5iQgflg-y6JA) (detailed)

### **2) Motivations & Use Cases**

There has been a paradigm shift towards Event Driven Architectures

![img](img/sMDgs7Ypn9LKP6ciZFiLxt01X9u25wGJrxaT_qQz7C88mwKQzllS7E95J5Ox6XF9J7YoerZs7qOuTpXTTDuxJt6lyHcURJRQrAJLEMflyH8MXPRXKdSjiCa619NAAefJupe6CDE3ScrmfB3RdOo4Ano.png)

To manage this shift, we need:

- A single platform to connect everyone to every event
- A real-time stream of events
- All events stored for historical view

**Apache Kafka** has become the industry standard (?) for real-time event streaming

[35% of the Fortune500 as of today]( https://kafka.apache.org/powered-by)

![img](img/a0D4ElQR4tEAVdJL-vcRukkaxyWh0LG8WOhFURY4Imdal-jmBgDVcqbUH0sPWb4ZN9A0qjcb-qJKdhXLmamw3nC7K_1IkkCa3lDuEhsHr6rG-4123Ws1EM9kSp-dvRtGimlZXjR1s2tKaG7xzEHEUV8.png)

**Application Examples:**

- **Banking**: Fraud detection - alert on your phone when you make a transaction
- **Banking 2:** Modernising legacy systems - tons of old batch processes ===> now moving towards immediate transactions
- **Automotive**: IoT - cars are distributed systems reporting tons of data, typically built on a real-time event-driven platform
- **Real-time e-Commerce:** Real-time analysis of what each customer is doing
- **Customer 360 (???)**
- **Online Gaming** 
- **Government**
- **Financial Services**

### **3) Apache Kafka Fundamentals**

![img](img/r3dMULMxFLmN_KVSrUWLTmfOBQA5iKOrcXnU87hAAlLb8jsD_fUAqltW1FKYKVovuU5kcB4sR98Sye8-dd20CKZPNrJcmaC2mnVD3xl_1nknqDRLrqi2E9QaTXg8gdnDLJUKXd7gArzCRrceNdcoXdk.png)

**Producers** - those client applications that publish (write) events to Kafka

![img](img/ijIod7jamOsIKepbM2mGK7QIelFnqMIXHsCPgQKb2fAbF2_vFxSHAbxqeBxuBB65HSLPn74HyL6UIdPlfPY37NeterlJX43v7wqLi74ofCtcLa2O3fOqLmNyPXN-x23Q1dqCCd8E1kSY0pO7ZY7C1v4.png)

**What’s in a Kafka Cluster?**

**Kafka Brokers** - allows consumers to fetch messages by topic, partition and offset.

<img src="img/CdCADAXM5_YKsO3i39Wgb6e87cmJElKFsJdEVsNikUoWz1OFF1ZXZiprg5U5f3NaxK6Tx5SpHhP2qDfcDd5Ld_jRUlBeL7lDynpnKSyN7iAMa0mFYlEFprgCG9Ii_d-HK-pKC2L6WVoo7bb65K6OzvU.png" width=75% />  

Brokers can be thought of in legacy terms as machines, or servers

**Consumers** - subscribe to (read and process) these events

![img](img/r_JvGXjJgou34jF4Ji2SdFLYc20j6n8j3S6eDOremkL3aNcmxz_VuExgaZnhJ-BMUy-jJ__Efp3d3H1SwcxxrYirP_6wSudhksuptg_Jl-_Pwr8rMoARUbCYNM3K-EzYchwb-Oyc4TMQD81A2k-htwk.png)

**Consumers, producers, Clusters (brokers)**

and **Zookeeper!**

**![img](img/WqwfJrQGNTTx5yPadARnR6CsQZ74-J1phUzrQTDW8j7aBcGTPsfgfdMELj1VULW0P_9qconqwDQvn-x8ydoZL4lN-yItXIOpAPzj4S7CXTPgP1wMnVOC8AL5nICEbpThm4Gw_XPjYU-LaXttMK1ZOwY.png)**



Zookeeper will eventually be deprecated 

**Producers** and **Consumers** are decoupled ===> they know nothing of each other

They don’t affect each other: 

- Slow consumers don’t make slow producers (vice versa)
- They scale independently 

A **Topic** is a collection of related messages (a log)

![img](img/AHh8WUtbUDAC4sVPOdpoBIHe6nycYFOFdPNIAfsybDOV7Y8zETg7qug2wxwAhytE_tQaY7cm5XILf5amXVb_L6KBSBkvLMn3o4OvW5dRIsn7svqPnvJfl3Mhocmexd2PInyPMlP6Ii_PSWi_OQUzuGQ.png)

You can, in theory, have unlimited topics

**Partitions**

![img](img/V-WY244MtauA6-2bR2Ve5DUkL7Fna8gJulGqVh91NLakyolHWzO_mFMgyQxZOQL9mwaoX8VEuM6fz6Eg38ZptLzgRawLqsl4ZcbQqtJp1xxq8T6xKJx4uhB0pK07m9Rajtfyzqzbecqhq2yA34Kk_qQ.png)

Split a topic up into partitions, which are allocated to brokers. This is what allows Kafka to scale.

Actually, a partition is a log (not a topic)

Partitions are ordered

Another view of partitions

![img](img/XnqfWcIP6G_H5BDyU0gQ-nuudwPoC9MWRnp-jK6MZ9MQQMg3BNgvbfSvaA4N3fjYiXoxCIUOr-dvtqKeQ3DP_tqBwtzCaH2VhXulb0IS16CMbL6BfmG_xBHeZ9GGdDA3ywm2frXd7LkpnCQTi2TlO4Q.png)

What is a log?

![img](img/AkLBZSB0PBWvRKwWBxfzIZg-OnQeN4tTDCp3c8vFI7ipKz6Ho7IkT90UQRHyjYVeLWhQU91HIjk7dhiCD_QE8Bh0y9t95j2Iv0pEVQn2cLid33bkcgvT6zKY6ItDHo-mXz-gmCxOa_VqnZ4dj7nuFMY.png)

Logs are only appended too

Logs are immutable

![img](img/xmiBCnHbSBE2ZDuUGXiLTX5jAy6K3o8Jr1jrIxa7ZMOt3QRhVG9Vc4YgSKk-IosHnZ-d_bNzQBSQoymVGrzBpSwm2PDfayC6L40gZTh6KKd_nKN38zTDDXod-nTyxgeVhl5b_5UQQdKSICEi6b0rAcs.png)

Topics can have a TTL (an expiry date)

Topics are also known as streams 

Every event (message) is a key-value pair

Every message has a timestamp

![img](img/aBujZxmxv72tej4jcMBTUU3PDipHp4XIYK8IILz_WdPSC5ykbMx80sjgA1Wo93WvMozltbAB4kWsMYEotKHE5hUTr8MRKvlh3BbKhP0dYkmsZ3aCrQw3KldepJ4GY1_UFsPXiLLXBmtrnNA8HTqVwb4.png)

Brokers manage partitions:

- Messages of topic are spread across partitions
- Partitions are spread across Brokers
- Each broker handles many partitions
- Each partition is stored on a Broker’s disk
- Partition {1..n log files}
- Each message in the log is identified by an *offset*
- Configurable retention policy

![img](img/h40d-Axk5xWURcJxF1vdRhemGyu0zDKP3uTsCBajQe_cVxEhEBX_3K20dvBuBKzPCH9saQz9_mTl_nzzate55fUrHP8IhTOSsv_DyiuVL4uVfJiZz71qk0n9xGd2OFuYVGLve06x7v8byn0HusmEj2A.png)

Broker’s are replicated (leader-follower strategy)

Producers write data as messages

Producers can be written in several languages

- Java (native), c/c++, python, go, .net, jms, …
- And more… (JS, etc.)
- REST proxy for unsupported languages

There is also a CLI producer tool

**Load Balancing and Semantic Partitioning**

Producers use a **partitioning strategy** to assign each message to a partition

- Load balancing
- Semantic partitioning

Partitioning strategy is specified by the producer

- Default: *hash(key) % number_of_partitions (% = mod)*
- No key → Round-Robin

^ Messages of the same key always land in order

Custom partitioner possible

**Consumer Basics**

Consumers pull messages from 1..n topics

New inflowing messages are automatically retrieved

Consumer offset (incase something falls down):

- Keeps track of the last message read
- Is stored in special topic

CLI tools exist to read from cluster

**Distributed Consumption**

**![img](img/cB4T71-TokmwJbQaO0ECU8oa2lMzmcImmB8hsx1NRG_Ri8oHxVWpgEVJou9pxDczK3GCdqRLkCm_PfRfhwxGTn2PxfQgaSTzEUkgk41DEOAhZlLD7QIHj3AUHEtef_oAtvsdioklumsBt249zup4dCg.png)**

**Every system you’ll ever build conforms to this diagram:**

**![img](img/eNsLWAqic6r4hTW11cIgeXUA5pQGYEgKm4rn-npWYxfA0h1l02l7PPgGcosz7r-lhx5FlisEi-oHOHc5NcITpE6Ey0cLnorrBW8K1EGxmt2I3JMIngOvfusfq0XtVWQyZ-E5SKNaqg9oRG2WdDZ7CDs.png)**

### **4) How Kafka Works**

[BasicProducer.java](https://youtu.be/jY02MB-sz8I?t=50) and [Consumer](https://youtu.be/jY02MB-sz8I)

![img](img/Yi0B5492ysCjiLfa6Cqnwip1a8xtg7N_-lQs99fz2uK0UAXkqpv5KIb5ITi3o77DEmcc5KpnuWzXyzNgw7aIIzq1A6KYySNCdCF56n9s3Hhgk7BByXbk96CMlh7u4Ag_gb5J6pqCGLGpkPq5bKz7g9M.png)

Topic1 is replicated over four brokers

Topic1 is the leader; the rest are followers 

 What happens when one broker goes offline? 

![img](img/Ke5t6_afRHbDnjJun3YgX8APHeVydnptlBOA8EjasSKdHCcqBHb9_xAt2WH9iQFTSj-fBhLSU58n79MbOSkBrZh-0lhm32VYYKbNdhOIK5OshZkUMcHfyVYOonQAKKUumJiC-fnMEi5_oHiFLylzB4Q.png)

Events are immutable

But, you don’t have the store them forever

Depends on: resources, Cost, GDPR, Business decisions, etc.

The default retention period is 7 days

**Producer Design**

![img](img/aAfOCFhQvwvfgnh_J_1kPOcDIlmRrLxr_5m2l-J9sgxIcIIaX2g08i3RrvR1wWoUBgNWB-RadbYEoorSSzdOLkNgPJCnQNNn7sfL2PmmQIM6PFYMhNtI1WgdO2U_30p-9ZvTm4xmj-V4dU5X_RQoBJA.png)



![img](img/REL8PvigzGS5AjNYQRULV8yOaXNQxjezWpXd_4bvNc3hDmByIMEFZG0K45J42E68umnZ7Sv0mLbbWbJnNZoCMeGqAQXclID_9T_QDu0J6hmaIDJ6Gqb0KRBHrIps_uZiAq9fjfrqNwoUTjTgkG4EqCc.png)



**At most once / At least once / Exactly once Paradigm**



![img](img/dRu8Bj4smtf4xEL8uRmdJ7HpX3XLoeYhl8T9OjX1nqZFTQ7gn0GPpEL3vngfksbRgZA4HkCOrdtoRfXg4_A1yG-5yOs_BXD7JoIGk_MCGp84CyV04NRxctRsf4oFNr4VCBNCU1S3zI07K_VZkZczwWA.png)



![img](img/-_xd84mAqF7pZmw7cVgm3o2geJ3Q3Z9dkIJU_7edIRaylQD9UhPC06AgrFtiQ94MJD24vGYIkX-A5ylhjUGV1QslyxvI1v40UK27sTUtgBrXEc-dBeCV_15LujNsboxSgV_zeDMR8oFLU5OQ7aDQaoo.png)

Idempotent - Gives the same result when performed

**Exactly Once Semantics**

What?

- Strong **transactional guarantees** for Kafka
- Prevents clients from processing duplicate messages
- Handles failures gracefully

**Use Cases**

- Tracking ad views
- Processing financial transactions
- Stream processing

**Consumer Groups**

One consumer group with two instances of the same consumer

![img](img/uEdtJ2io6TO9e0KebsxtVLLSHhRiqPy3AVwLosvr51xfwuEmZSG4CRBJKLUdim-7U_rOHjAfPuSMpaDs9JsU9cbR74doBO8csjgySJvbEl830OBjp1A-sVvyIoiQvqCPhiA5HhrveV1Q_vbhrEDEDGs.png)

[Consumer Groups](https://youtu.be/jY02MB-sz8I) - What happens when the composition of the group changes?

**Compacted Topics** 

**![img](img/PqWrxIbZyl_DZCAYTdvQe608l1HrEJ1__CUW_I3LQdGunTH1tj17PIrJ4Eg2BVmTzZnNxZTMyAGFA1ElD8bx9aGTLaNyeHOUGlPN4FsjNerOvR_8p6XLF9pf91LwNCjR-pw8cjfq7GScbU640g59LM8.png)**

^ Good when you’re interested in the most recent value

**Troubleshooting**

- Confluent Control Center
- Log Files
- Special Config Settings
- SSL logging
- Authorizer debugging

**Security** 

- Kafka supports encryption in transit
- Kafka supports authentication and authorisation
- No encryption at Rest out of the box!
- Clients can be mixed with & without Encryption & Authentication

### 5) Integrating Kafka into Your Environment

What is Kafka (really basic definition) - a distributed log with *producers* and *consumers* 

**Kafka Connect** is a data integration framework - gets data in and out of Kafka to systems which aren’t Kafka

<img src="img/AAuDTlQByqVi-o3816l0GB6qg26L_dGyhdgL5lrRQk6c6TO8-K9mg3xLP7KeGGhXx3jikPZFgotMPHCj1jZh4F6DvTfMVKDlXxHU96TtCbq2hA_M6vK9TbhwIgagYGJ2LpOpbt7s2H_oTsKGkbTYX7M.png" alt="img" width=67% />

**Sources and Sinks**

**![img](img/9d2biC0a8iHOpLIeRhBdd9g2gulEQrv2O6bRA2Vnesk3zcUWNYFm6tSmz4O5t4bda9DY5er01_P4VWZuXNqL-aSyvdK6UDNxDC0mwP0AOfqhVNSbH63Fz4BEHY8j4d6ACAEV9sUQwYTOm00jLUcDqY0.png)**

**Kafka Connect** runs in tasks across workers 

<img src="img/oYLtLJkcEWPsUDXMXEj-v9KEZ1JDUCi9c4w6XozEEknkqPI-NCU1lQVSw0leOZJ3AN0EUDkuok_9blezRSA0T7o5UIeSW77tdyuQ-a1hjO38ul-knWhvKatJyl9WNanJvXyLJPHS0CRVfuS6w8Cjxeo.png" alt="img" width=67%/>

In general, connectors can be parallized

**Confluent REST proxy** - a REST wrapper around the producer and consumer

It can talk to **non-native** Kafka apps

![img](img/YGSJXj5HFPv2EAMqtOAlopViYTTK4sQXyX-S2S0epjF9CvqJTA6d85Yu0grToevURzl9xyQWx-A0UHc3bWEPeZpL-SUvh88cBEIvM2sMOOBiZ3Eu5PRlWLxb4DlCvYQChobBzQpHl7afYEGgzxkemh8.png)

**The challenge of Data Compatibility at Scale**

Schema evolution has always been difficult ===> **Common schema registry** 

*The schema is always going to change*

![img](img/yNBMH_Rsop9yK54sY7Ijy9g7oVTD5D2o0B8wYoXe109acjKnRCmTDWh7BVEPnlIbFPYPvZAYJOFYD9Zv3FQeHfGhGkwvFfFtMziGLz5Xu0x7-jIJxcoS87Eub9wonmDE4kape5OfNAW5BV_7I8iI_Lw.png)

- Define the expected fields for each Kafka topic
- Automatically handle schema changes (e.g. new fields)
- Prevent backwards incompatible changes
- Support multi-data center environments

https://en.wikipedia.org/wiki/Apache_Avro

<img src="img/k2QYJn5reEph_D8NPnNQyZxsoAlcLDi6zJs_9wxdZsPudMiu4L_ibDsDTbGDEb-SVqkujz10dckDYj7n183pdJ_mGa56Hrbsu6MlKeJZ2z0EganuNB4BAGLIWOI1GgZ3wFpAhkP1kg4IAZFoQT_miQs.png" alt="img" width=67% />

**Versioned schema**

<img src="img/D2LGcah46fsP0zGYHFb7XrbyWORd3DKQvVMzuEoYnxkRf2UFGVdObmyEi-8iyk5n8m1n3tpxOoBMHP-_vIulTXYfDf0ZY51Za2ZRaVRxZ-lw6gqvv2yduNVjWb8kyiOklITX8YMj_vZaVmbp0pVw2Q4.png" alt="img" width=67% />

Etc.

**Confluent ksqlDB - SQL engine for Kafka**

```sql
CREATE STREAM vip_actions AS
SELECT userid, page, action
FROM clickstream c
LEFT JOIN users u ON c.userid = u.user_id
WHERE u.level = ‘Platinum’;
```

Leverage Kafka Streams API without any coding required

Use cases:

- Streaming ETL
- Anomaly detection
- Event monitoring

**Your Kafka Streams App**

**<img src="img/SFL7OjR1SNZi0EyiKexks4T4Ot6pOFTFi7FqH-bVdG3G3QhAoXgXvsnrWLwbOGPe7b2gY4ESfLwHI2LUrrNucyq4Fz_slIAPPOKW-1NN1AuJ6WfceIpSnLw6QfVsO415NbAVuSdM1w-RNc5LoFnN2Yc.png" alt="img" width=50% />**

<img src="img/ypLhCayUdkQOXDJ-zalxAZq07EpR_5kuo035UEl_kSmx4C0t7VCm8Ty2L0wD7m7mF-AWoL93kDJP1DEtKJpq4oWU6P05108W0TGOPmvDJD2gyVkjcjfEepnO-9aXmy0DBrrIQXEKeMTqzNzng8hNOaY.png" alt="img" width=50%; />

**Choose where you want to live on this continuum to do your stream processing**

### **6) The Confluent Platform** 

**Central Nervous System**

<img src="img/pkB76SSTq2-E9D900CwhkjQgcAwtnI1ZR1yWh9awtGXJYU9FHruNr9fq0-Acoi1Wx-MvNuE3NpWGnZEP5Rg28dBRD9QvPKBAJJPoSw5eW752Yve71nQmCx3IxL2Yj51NjyUHAk276pgE7By_2L0vl9k.png" alt="img" width=67%; />

**Investing in The Confluent Ecosystem**



**![img](img/QI5I4XQBvclD-PuFMjhGUVe0kFYPIVjPUJ_cVouS5ik3ohZgWn3I4r9L7K7H2LR7EvejBKNwjZd8Iv81WaqaNOdBYzpSVIAPDJGe3WtpSVEd5Hi5j-VNURB3aMrtGV9GLBfVXrqGiKKn2gEPNr6_6Hs.png)**

**===> Adopting a streaming-first Paradigm is the end game**

![img](img/D73YQbYoIHPy_UEo_vpkijDIgCvie4M9nqy4cCBuumaomob6sKm6G_hORPhkMihdW8Q65CisHtllEx6sNb0tGlwtfQKBWND4E-DDdA3ll25wVlIuYm5hddVqsFnPslfuDC1GXAJrra0UpuF2dBopG28.png)

Kafka can be deployed entirely on your hardware (kubernetes) if you want

Or, use *Confluent Cloud*

*![img](img/gBtuz6mt9nAd5hx75u4QpK2w8wnCmQr-dAQMpB_bTXP05mJJdrAkRz78IeryMm8yJNoYchja5InMb_7Py8yjNEjwDdCRmsWbcmxDn0U_FcdLk6c1VQ2aW1rViytlQhX820S-NVoZQBUFMoOdQUgqmVo.png)*

**Confluent Control Center** 

- Monitor system health of your Kafka cluster with curated dashboards
- Monitor data streams with end to end views of message delivery
- Manage Kafka topics and Kafka Connect operations 

**Confluent CLI** - manage your Confluent Platform deployment

**Role Based Access Control**

**Confluent Operator** - for those running on Kubernetes

![img](img/jOC0FrHOK21orN3uJr7rtFnhVuq-w_oK0rV5S99HlyzmuKNe58VzDhrU8n_u_az5eFnigP3SbK2BZ_u2BhujHHrbHkXRfVMpmpbr5dbOZG3y6tpQSTYs9N565h_FU03n6IIcgm_HctRJ-TL4B9cp_FY.png)

**Broad Connector Eco-System** 

**![img](img/tIdS7_U_Z4e-zY6ARUbDVpqIa7YYY7NHGoI5q5qTilxNTeTDwVeHnxJjJA7LbCQ2Qdhp7blut_QNOL0FGMPWf9p-tBnDH-Sq-dJsBH9NfCHy2A8D2Jat-Kch_kyVThiDhQ_fJbhHL1BOsmSl-GZgocs.png)**

[**Confluent Hub**](https://www.confluent.io/hub/?utm_medium=sem&utm_source=google&utm_campaign=ch.sem_br.brand_tp.prs_tgt.confluent-brand_mt.xct_rgn.emea_lng.eng_dv.all_con.confluent-hub&utm_term=confluent hub&creative=&device=c&placement=&gclid=EAIaIQobChMI8su6hOCU-QIVHwIGAB1-ogCnEAAYASAAEgKvrPD_BwE) **-** Kafka Connectors

The Confluent Platform helps drives Kafka into the business

### **7) Conclusion**

We have discussed: 

- Topics and Partitions
- Brokers
- Producers
- Kafka Clusters
- **Stream** vs Batch processing

http://confluent.io/training

==> Apache Kafka Admin 

==> Confluent Developer Skills for Building Apache Kafka

==> Stream Processing using ksqlDB & Apache Kafka Streams

==> Confluent Advanced Skills for Optimizing Apache Kafka