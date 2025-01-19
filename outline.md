# FRESCO: A Public Multi-Institutional Dataset for Understanding HPC System Behavior and Dependability

## Abstract
> High performance compute and distributed computing systems are now fundamental to scientific research, from academic institutions to industrial applications. However, publicly available operational data from these systems remains scarce, as private sector organizations, which operate many large-scale computing facilities, rarely share detailed system metrics and failure data. While datasets like USRC's exist, they primarily focus on failure events alone. This scarcity severely limits research in critical areas such as system dependability and resource optimization. To address this gap, we present FRESCO, a comprehensive dataset collected from multiple university computing clusters that captures detailed operational metrics in a time-series format. The dataset features six key measurement metrics (CPU usage, GPU usage, memory usage, memory usage excluding disk cache, NFS usage, and block I/O) paired with sixteen job-specific attributes including submission time, resource allocation, and job exit codes. Extracted using XDMoD, FRESCO provides researchers unprecedented access to real-world computing cluster behavior, enabling in-depth analysis of resource utilization patterns, failure modes, and system performance. The dataset's granular structure, combining both resource metrics and job outcomes, makes it particularly valuable. To certify the value of our dataset, we demonstrate its utility through (here's a few ideas)

- Idea 1: characterization of job failure patterns and their correlation with resource utilization
- Idea 2: identification of resource contention patterns that impact job completion success rates (e.g., does high memory and high block I/O (or CPU + memory or CPU + block I/O) demonstrate resource contention leading to higher failure rates?)
- Idea 3: characterization of job failure patterns in relation to overall workload (i.e., does the number of concurrent jobs running impact the job failure rate?)

## Introduction
### Problem Statement
- The Current State and Significance:
  - HPC and distributed computing systems are now fundamental infrastructure for scientific research, industry, and academia 
  - The scale and complexity of these systems continues to grow 
  - Understanding system behavior, resource usage patterns, and failure modes is critical for:
    - Maintaining system reliability 
    - Optimizing resource allocation 
    - Improving job completion rates 
    - Reducing operational costs

- The Core Problem:
  - There is a critical lack of publicly available operational data from production HPC systems 
  - Private sector organizations rarely share detailed system metrics and failure data 
  - Existing public datasets (like USRC) focus narrowly on failure events without the broader operational context 
  - This data scarcity creates a significant barrier for research in:
    - System dependability 
    - Resource optimization 
    - Failure prediction 
    - Performance modeling

- The Gap in Current Solutions:
  - Most existing datasets lack the combination of:
    - Detailed resource utilization metrics 
    - Job-specific attributes 
    - Failure data 
    - Cross-institutional standardization 
  - Current approaches to studying HPC system behavior are limited by:
    - Incomplete data about system state before failures 
    - Insufficient context about resource utilization patterns 
    - Lack of standardized metrics across different institutions

- The Impact
  - This data scarcity impedes:
    - Development of better failure prediction models 
    - Understanding of resource contention patterns 
    - Optimization of job scheduling algorithms 
    - Research into system dependability 
  - The community lacks the empirical foundation needed to develop and validate new approaches to HPC system management

### Research Questions:
How do resource utilization patterns affect job outcomes? What are common failure modes in academic HPC systems?  How can we improve system dependability?
### Contributions:
- Novel Dataset Characteristics:
  - First multi-institutional dataset that combines:
    - Detailed operational metrics (CPU, GPU, memory, NFS, block I/O)
    - Complete job lifecycle information 
    - Standardized metrics across different institutions 
    - Rich contextual data about resource allocation and usage 
  - Comprehensive temporal coverage:
    - Continuous time-series format 
    - Captures both normal operations and failure events 
    - Enables analysis of system behavior over time 
    - Allows correlation between resource usage and job outcomes

- Methodological Contributions:
  - Standardized approach to collecting and organizing HPC metrics:
    - Unified data collection methodology using XDMoD 
    - Consistent metric definitions across institutions 
    - Reproducible collection process 
    - Validated data quality assurance procedures

- Analysis Framework? This section will depend on what analysis is done.
  - Novel analytical approaches demonstrated through:
    - Resource contention pattern identification 
    - Job failure correlation analysis
    - Workload impact assessment
  - Reusable analytical methodologies for:
    - System behavior characterization 
    - Failure pattern identification 
    - Resource utilization optimization

- Community Impact:
  - Open access to production HPC operational data
  - Enables new research in:
    - Failure prediction and prevention 
    - Resource allocation optimization 
    - Job scheduling algorithms 
    - System dependability analysis 
  - Provides benchmark data for:
    - Comparing system performance across institutions 
    - Validating new HPC management approaches 
    - Evaluating optimization strategies

- Practical Applications:
  - Direct applications for:
    - System administrators (resource management)
    - Researchers (research areas, performance optimizations, etc.)
    - Policymakers (resource allocation)
  - Tools and documentation for:
    - Dataset utilization 
    - Analysis reproduction 
    - Extension to other institutions

## Related Work
### Existing HPC Datasets and Their Limitations

The landscape of publicly available HPC system datasets is limited, with most existing collections focusing on narrow aspects of system behavior or specific failure modes. The USRC dataset, released in 2005, pioneered the public sharing of HPC failure data but primarily captures failure events without broader operational context. While valuable for basic failure analysis, it lacks the granularity needed to understand complex system interactions and modern operational patterns.

Recent contributions include large-scale disk failure datasets, comprising over 5,000 failure records from more than 40,000 disks collected over five years. These datasets have advanced our understanding of storage subsystem reliability but are limited in scope, focusing solely on storage components without integration into broader system metrics.

Current datasets face several key challenges:
- Unstructured log formats that complicate analysis
- Poor standardization across institutions
- Limited scope, often focusing on single subsystems
- Lack of operational context around failure events

### HPC System Analysis Studies

#### Current Analysis Approaches
Traditional fault-tolerance strategies like checkpointing and replication have been the mainstay of HPC system reliability. However, as systems grow in scale and complexity, these reactive approaches prove insufficient. Modern HPC environments require proactive failure management strategies based on comprehensive system understanding.

Here are the key limitations that make these reactive approaches inadequate for modern computing environments:

##### Scale-Related Issues

- Growing Data Volume
  - Modern HPC jobs handle petabytes of data
  - Checkpointing this volume of data takes significant time
  - The time to write checkpoints can exceed the mean time between failures
  - Example: If checkpointing takes 2 hours and system failures occur every 1.5 hours on average, the system spends more time checkpointing than computing

- Resource Overhead
  - Replication requires 2x or 3x resources for redundancy
  - At large scales, this becomes prohibitively expensive
  - Example: A job needing 1000 nodes would require 2000-3000 nodes with replication
  - Storage requirements double or triple

##### Complexity-Related Issues

- Interdependent Failures
  - Modern HPC systems have complex interconnected components
  - Failures in one subsystem can cascade to others
  - Reactive approaches can't prevent these cascade effects
    - Example: A network issue might cause multiple nodes to fail simultaneously, affecting all replicas

- Multiple Failure Modes
  - Systems face varied failure types (hardware, software, network)
  - Each type requires different recovery strategies
  - Reactive approaches treat all failures similarly
  - Can't optimize recovery based on failure type

##### Performance Impact

- Increasing Overhead
  - More frequent checkpointing needed as systems grow
  - Higher overhead from I/O operations
  - Network congestion from checkpoint traffic
    - Example: A system might spend 30% of its time just managing checkpoints

- Resource Contention
  - Multiple jobs competing for I/O resources during checkpointing
  - Network bandwidth limitations
  - Storage system bottlenecks

##### Modern Workload Challenges

- Dynamic Resource Needs
  - Modern applications have varying resource requirements
  - Reactive approaches assume static resource needs
  - Can't adapt to changing workload patterns

- Real-time Requirements
  - Many applications need real-time processing
  - Cannot afford the delay of reactive recovery
  - Time to restore from checkpoints may exceed acceptable latency

##### Cost Implications

- Operational Costs
  - High energy consumption from redundant computation
  - Storage costs for checkpoint data
  - Additional hardware for redundancy
    - Example: Doubling hardware and energy costs for replication

- Management Complexity
  - Increased system administration overhead
  - More complex scheduling systems needed
  - Higher maintenance costs

#### Performance Analysis Methods
Current performance analysis techniques face several limitations:
- Difficulty in capturing real-time system behavior
- Challenges in correlating metrics across subsystems
- Impact of varying system architectures on analysis
- Limited benchmarking approaches for modern workloads

### Resource Utilization Analysis

#### Common Metrics
HPC environments typically track several key metrics:
- CPU utilization and threading patterns
- Memory usage and page faults
- I/O operations and bandwidth
- Network utilization
- Power consumption

#### Time-Series Analysis
Understanding temporal patterns in resource utilization is crucial for system optimization. Current approaches focus on:
- Statistical analysis of usage patterns
- Correlation between different metrics
- Trend analysis and forecasting
  However, these methods often lack the granularity and breadth needed for comprehensive system understanding.

### Job Failure Analysis

#### Current Methods
Existing approaches to job failure analysis include:
- Statistical correlation between resource usage and failures
- Machine learning for failure prediction
- Pattern recognition in system logs

These methods are limited by:
- Incomplete data about system state
- Lack of standardization in failure categorization
- Limited integration with operational metrics

#### Real-time Detection Challenges
Real-time failure detection faces several obstacles:
- Processing large volumes of monitoring data
- Balancing detection accuracy with timeliness
- Integration with job scheduling systems
- Resource overhead of monitoring systems

### Gap Analysis

#### Current Limitations
The field faces several significant limitations:
- Lack of standardized metrics across institutions
- Missing operational context in failure data
- Limited public availability of comprehensive datasets
- Poor integration between different monitoring systems

#### Need for FRESCO
FRESCO addresses these limitations through:
- Unified approach to data collection and organization
- Integration of operational metrics with job outcomes
- Multi-institutional scope with standardized metrics
- Comprehensive coverage of system behavior


## Dataset Description

### Data Collection Methodology

#### Collection Framework
- Data collected using XDMoD (Open XDMoD) monitoring framework
- Collection period spans [TIME PERIOD]
- Data gathered from multiple university computing clusters
- Automated collection process to ensure consistency

#### Data Sources
- Resource usage metrics from system monitoring tools
- Job information from scheduler logs
- Error and failure logs from system logs
- Performance counters and hardware metrics

#### Anonymization Process
- Sensitive information removal (usernames, group names, job names)
- Consistent anonymization across institutions
- Preservation of relationships between data points
- Documentation of anonymization methodology

### Dataset Structure

#### Core Measurement Metrics
1. CPU Usage
    - Per-core utilization
    - Thread-level statistics
    - Load averages

2. GPU Usage
    - Utilization rates
    - Memory usage
    - Temperature metrics

3. Memory Usage
    - Total consumption
    - With and without disk cache
    - Page fault statistics

4. Network File System (NFS) Usage
    - Read/write operations
    - Bandwidth utilization
    - Connection statistics

5. Block I/O
    - Disk read/write operations
    - I/O wait times
    - Queue lengths

#### Job Attributes
- Submission time
- Start time
- End time
- Time limit
- Number of hosts
- Number of cores
- Account/group information
- Queue type
- Host list
- Exit codes
- Resource allocations

#### Time Series Format
- Sampling interval: ????
- Timestamp precision
- Data alignment across metrics
- Handling of missing data points

### Quality Assurance

#### Completeness Checks
- Coverage analysis across time periods
- Missing data identification
- Gap analysis and documentation
- Cross-institutional data consistency

#### Known Limitations
1. Data Granularity
    - Sampling frequency limitations

2. Institutional Variations
    - Hardware differences
    - Configuration variations
    - Policy differences
    - Workload characteristics

### Dataset Statistics
- Total time period covered
- Number of job records
- Volume of metric data
- Distribution of job types
- Failure statistics
- Resource usage patterns

### Access and Usage
- Data format specifications
- Access procedures
- Usage guidelines
- Citation requirements
- Tool recommendations

## Analysis Methodology
- Data preprocessing steps
- Analysis techniques
- Metrics definitions
- Statistical methods used

## Results and Discussion

### For Idea 1 (Job Failure vs Resource Usage):
- Analysis of job failure distribution
- Correlation between resource utilization metrics and failures
- Identification of resource usage patterns preceding failures
- Implications for failure prediction and prevention

### For Idea 2 (Resource Contention Impact):
- Analysis of concurrent resource usage patterns
- Investigation of resource contention scenarios
- Memory + Block I/O combinations
- CPU + Memory combinations
- CPU + Block I/O combinations
- Impact of resource contention on job completion rates
- Variations across different queue types
- Implications for resource allocation and scheduling

### For Idea 3 (Workload Impact):
- Analysis of concurrent job patterns
- Correlation between number of concurrent jobs and failure rates
- Investigation of peak workload periods
- Impact of system load on job success rates
- Variations by job type and queue
- Implications for workload management

### Each of these sections might include:
- Detailed statistical analysis
- Relevant visualizations
- Discussion of findings
- Practical implications


## Applications
- Research Applications
- System Administration Uses
- Policy Implications
- Future Research Directions

## Known Issues and Limitations
- Dataset Limitations
- Analysis Constraints
- Generalizability Considerations


## Conclusion
- Summary of Contributions
- Future Work
- Dataset Availability
