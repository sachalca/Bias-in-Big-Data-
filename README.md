# Biases in Big Data

This project explores how bias can enter large-scale data systems and be amplified through machine learning pipelines, using the loan approval process as a case study. The analysis is inspired by Cathy O'Neil’s *Weapons of Math Destruction*, which highlights how data-driven algorithms can cause widespread harm when deployed without ethical scrutiny.

The central question is:  
Is the loan approval process biased based on gender, marital status, education level, age, technological access, or car ownership?

## Methodology

Two datasets were used:
- `application_data.csv` (37 MB)  
- `previous_application.csv` (78 MB)  

These were joined on the loan ID to create a unified view of each applicant's current and past loan applications. After cleaning, the analysis focused on key features related to potential bias.

The project was executed in two phases:
1. Small-scale: Run locally in a Jupyter notebook using a filtered dataset.
2. Large-scale: Full dataset processed using PySpark on Amazon EMR to simulate a production-scale data pipeline.

The code computes multiple fairness metrics manually using Spark RDDs, including:
- Grouped approval rates
- Disparity ratios
- Frequency of denial across demographic subgroups

## Results

Key findings include:
- Gender Bias: Approval rates were slightly lower for female applicants. However, the disparity was not large enough to suggest hard-coded discrimination, though it raises flags worth investigating.
- Marital Status & Car Ownership: These attributes showed stronger correlations with approval likelihood, suggesting potential proxy bias—where non-sensitive attributes inadvertently encode sensitive patterns.
- Technological Access: Applicants without mobile devices or email access were approved at significantly lower rates, implying digital exclusion could affect access to credit.

## Conclusion

Even without malicious intent, big data systems can replicate or worsen social inequities due to biased training data or flawed assumptions. This project emphasizes the importance of auditing data pipelines for fairness before deployment—especially in finance, where decisions have real-world consequences.

## Technical Stack

- Python, Jupyter, PySpark
- AWS EMR (for distributed computation)
- Manual RDD-based implementation of fairness metrics

Author: Sacha Le Clainff Alonzo  
