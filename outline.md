# FRESCO: A Public Multi-Institutional Dataset for Understanding HPC System Behavior and Dependability

## Abstract
> High performance compute and distributed computing systems are now fundamental to scientific research, from academic institutions to industrial applications. However, publicly available operational data from these systems remains scarce, as private sector organizations, which operate many large-scale computing facilities, rarely share detailed system metrics and failure data. While datasets like USRC's exist, they primarily focus on failure events alone. This scarcity severely limits research in critical areas such as system dependability and resource optimization. To address this gap, we present FRESCO, a comprehensive dataset collected from multiple university computing clusters that captures detailed operational metrics in a time-series format. The dataset features six key measurement metrics (CPU usage, GPU usage, memory usage, memory usage excluding disk cache, NFS usage, and block I/O) paired with sixteen job-specific attributes including submission time, resource allocation, and job exit codes. Extracted using XDMoD, FRESCO provides researchers unprecedented access to real-world computing cluster behavior, enabling in-depth analysis of resource utilization patterns, failure modes, and system performance. The dataset's granular structure, combining both resource metrics and job outcomes, makes it particularly valuable. To certify the value of our dataset, we demonstrate its utility through (here's a few ideas)

- Idea 1: characterization of job failure patterns and their correlation with resource utilization
- Idea 2: identification of resource contention patterns that impact job completion success rates (e.g., does high memory and high block I/O (or CPU + memory or CPU + block I/O) demonstrate resource contention leading to higher failure rates?)
- Idea 3: characterization of job failure patterns in relation to overall workload (i.e., does the number of concurrent jobs running impact the job failure rate?)

## Introduction
### Problem Statement
- Elaborate on the need for public HPC operational data. 
  - "While datasets like USRC's exist, they primarily focus on failure events alone. Private sector organizations, which operate many large-scale computing facilities, rarely share detailed system metrics paired with failure data".
- Current challenges in HPC system analysis.
### Research Questions:
How do resource utilization patterns affect job outcomes? What are common failure modes in academic HPC systems?  How can we improve system dependability?
### Contributions:
- Dataset description and scope
> - First multi-institutional dataset combining both detailed operational metrics and job outcomes
> - Standardized approach to collecting and organizing HPC metrics across different institutions
- Analysis methodology
- Key findings


## Related Work

1. Existing HPC datasets
> - USRC dataset (historical performance and failure data, released 2005)
> - Large-scale disk failure dataset (5,000 failures from 40,000 disks over 5 years)
> - Challenges with current datasets (unstructured logs, poor standardization)
2. HPC system analysis studies
> - Current approaches to fault prediction and analysis
> - Limitations of traditional fault-tolerance strategies like checkpointing
4. Resource utilization analysis
> - Common metrics tracked in HPC environments
> - Importance of time-series data for operational analysis
4. Job failure analysis
> - Current methods for correlating resource usage with failures
> - Challenges in real-time fault detection
5. Gap analysis showing need for FRESCO
> - Lack of standardized, comprehensive datasets across institutions
> - Need for combined operational metrics and job outcome data
> - Limited availability of public HPC operational data


## Dataset Description
### Data Collection
- Collection methodology using XDMoD.
- Time period and scope.
> - Compare scope to existing datasets (e.g., USRC's historical data)
- Anonymization process.

### Dataset Structure
- Measurement metrics explanation
> - Context for why these specific metrics were chosen based on industry standards
- Job attributes
- Time series format details
> - Justification for time-series format based on analytical needs

### Quality Assurance
- Data validation methods
> - Add comparison of data validation methods with other public datasets
- Completeness checks
- Known limitations -> data granularity and sample collection irregularity

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
