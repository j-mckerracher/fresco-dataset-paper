# FRESCO: A Public Multi-Institutional Dataset for Understanding HPC System Behavior and Dependability

## Abstract
Supercomputer and distributed computing systems are now fundamental to scientific research, from academic institutions to industrial applications. However, publicly available operational data from these systems remains scarce, as private sector organizations, which operate many large-scale computing facilities, rarely share detailed system metrics and failure data. This scarcity severely limits research in critical areas such as system dependability and resource optimization. To address this gap, we present FRESCO, a comprehensive dataset collected from multiple university computing clusters that captures detailed operational metrics in a time-series format. The dataset features six key measurement metrics (CPU usage, GPU usage, memory usage, memory usage excluding disk cache, NFS usage, and block I/O) paired with sixteen job-specific attributes including submission time, resource allocation, and job exit codes. Extracted using XDMoD, and anonymized by us, FRESCO provides researchers unprecedented access to real-world computing cluster behavior, enabling in-depth analysis of resource utilization patterns, failure modes, and system performance. The dataset's granular structure, combining both resource metrics and job outcomes, makes it particularly valuable. To certify the value of our dataset, we demonstrate its utility through (undecided at this point, but I’m only going to choose one idea.)
- Idea 1: characterization of job failure patterns and their correlation with resource utilization
- Idea 2: evaluation of user accuracy in estimating job runtime requirements
- Idea 3: identification of resource contention patterns that impact job completion success rates.

## Introduction
### Problem Statement
Elaborate on the need for public HPC operational data. Current challenges in HPC system analysis.
### Research Questions:
How do resource utilization patterns affect job outcomes? What are common failure modes in academic HPC systems?  How can we improve system dependability?
### Contributions:
- Dataset description and scope
- Analysis methodology
- Key findings


## Related Work

1. Existing HPC datasets 
2. HPC system analysis studies 
3. Resource utilization analysis 
4. Job failure analysis 
5. Gap analysis showing need for FRESCO


## Dataset Description
### Data Collection
- Collection methodology using XDMoD. 
- Time period and scope.
- Anonymization process.

### Dataset Structure
- Measurement metrics explanation
- Job attributes
- Time series format details

### Quality Assurance
- Data validation methods
- Completeness checks
- Known limitations -> data granularity and sample collection irregularity

## Analysis Methodology
- Data preprocessing steps
- Analysis techniques
- Metrics definitions
- Statistical methods used

## Results and Discussion

### For Idea 1:
- Job Failure Pattern Analysis
- Resource Utilization Correlation
- Failure Prediction Implications

### For Idea 2:
- Runtime Estimation Analysis
- User Behavior Patterns
- Scheduling Implications

### For Idea 3:
- Resource Contention Analysis
- Impact on Job Completion
- System Optimization Implications


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
