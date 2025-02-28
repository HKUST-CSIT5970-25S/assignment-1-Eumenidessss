[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name:  ZHAN Yajing
### Student Id: 21074664
### Email: yzhanai@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    > Your answer goes here.
    > 
    > **Answer:**
    > 
    > I used **Phoronix Test Suite v10.8.4** as the measurement tool. It is an open-source benchmarking software that can test the performance of multiple system components, including CPU, memory, disk, and GPU. To measure CPU and memory performance, I selected the **`pts/compress-7zip`** and **`pts/ramspeed`** benchmarks.
    > 
    > #### Benchmark Suite:
    > - **`pts/compress-7zip`**: This benchmark is primarily used to test the CPU performance in compression tasks. It simulates the CPU’s processing power under high compression ratio tasks, especially its ability to handle compression algorithms. Through this test, we can assess how efficiently the CPU handles data compression.
    > 
    > - **`pts/ramspeed`**: This benchmark focuses on testing the memory bandwidth performance. It evaluates the speed and bandwidth of memory access by performing memory read and write operations, reflecting the system’s performance under memory-intensive tasks.
    > 
    > #### System Configuration:
    > - **`pts/compress-7zip`**: This test by default uses multithreading to simulate high-load compression tasks, testing how the CPU handles parallel processing under different thread counts.
    > 
    > - **`pts/ramspeed`**: This test by default uses different memory access patterns to measure memory bandwidth, offering various memory operations like sequential and random read/write to fully understand memory performance.
    > 
    > #### Explanation of Measurement Results:
    > - **CPU Performance**: The results from the CPU test represent the processing power of the CPU under load, typically expressed in operations per second or a performance score based on system responsiveness.
    > 
    > - **Memory Performance**: The values from the memory test represent memory bandwidth, indicating the speed at which the system reads from or writes to memory.
  
2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | --------------- | ------------------ |
    | `t2.micro` |  Compression: 3614 MIPs   Depression:2958 MIPs    |     10438.53 MB/s       |
    | `t2.medium`  | Compression: 8822 MIPs   Depression: 6128 MIPs       |  19038.86 MB/s       |
    | `c5d.large` |Compression: 7538 MIPs    Depression: 4886 MIPs    |          13944.94 MB/s          |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.
    >
    > Based on the test results, T2.medium performs the best in both CPU and memory performance, especially in memory bandwidth, outperforming the other two instance types. T2.micro has weaker performance, while C5d.large is stronger in computational performance but slightly inferior to T2.medium in memory performance.
## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` |      3560      |  0.374   |
    | `m5.large` - `m5.large`   |      9220      |  0.108   |
    | `c5n.large` - `c5n.large` |      4960      |  0.181   |
    | `t3.medium` - `c5n.large` |      2110      |  0.777   |
    | `m5.large` - `c5n.large`  |      4940      |  0.184   |
    | `m5.large` - `t3.medium`  |      1990      |  0.835   |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.
    >
    > Between instances of the same type, the TCP bandwidth is higher and the RTT is lower, indicating better network performance. However, between instances of different types, the TCP bandwidth decreases and the RTT increases, resulting in poorer network performance. This is primarily due to differences in hardware and network configurations between the instance types.
2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      |      3140      |  61.903  |
    | N. Virginia - N. Virginia |      2530     |  0.208  |
    | Oregon - Oregon           |      4950      |  0.167   |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
    > 
    > Based on the test results, network latency is lower and bandwidth is higher within the same region. However, cross-region connections experience increased latency and reduced bandwidth.
