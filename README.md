# A/B Testing Simulation for Marketplace Platform

## Introduction

This project simulates an A/B test to evaluate a new ranking algorithm for job requests on **The Guild**, a fictional gig marketplace platform. The goal is to compare the current algorithm (Control) against the new algorithm (Treatment) to determine if it improves the **Top-K Acceptance Rate** while maintaining stability in guardrail metrics.

## Table of Contents

- Introduction
- Requirements
- Usage
- Project Structure
- Experiment Design
- Metrics
- Hypothesis
- Data Generation
- Simulation Code
- Results and Analysis
- Conclusion
- Recommendation

## Requirements

To run this simulation, you’ll need:

- Python 3.x
- Jupyter Notebook
- The following Python libraries:
  - `numpy`
  - `pandas`
  - `matplotlib`
  - `statsmodels`
  - `scipy`

Install them using:

```bash
pip install numpy pandas matplotlib statsmodels scipy
```

## Usage

1. Open the Jupyter notebook `ab-testing-simulation.ipynb`.
2. Run all cells sequentially to execute the simulation and analysis.
3. Review the generated plots and statistical results.
4. Refer to the conclusion and recommendation sections for insights.

## Project Structure

- `ab-testing-simulation.ipynb`: Main notebook containing simulation code, analysis, and results.

## Experiment Design

- **Variants**:
  - **Control (A)**: Current ranking algorithm.
  - **Treatment (B)**: New ranking algorithm.
- **Triggering**: Suppliers are randomly assigned to Control or Treatment upon viewing the job list.
- **Run-Time**:
  - Duration: 22 days.
  - Sample Size: 50 eligible suppliers per group per day (1056 total per group). Eligibility requires viewing at least 5 job requests per session.

## Metrics

### Target Metric

- **Top-K Acceptance Rate (K=3)**:
  Percentage of accepted jobs ranked in the top 3 positions.
  - **Formula**: Top-K Acceptance Rate = (Number of accepts within top K positions) / (Total number of accepts)
  - **Goal**: Increase.

### Guardrail Metrics

- **Overall Acceptance Rate**:\
  Proportion of job requests accepted.
  - **Formula**: Overall Acceptance Rate = (Number of accepted job requests) / (Total number of job requests)
  - **Goal**: Stay stable or improve.
- **Time to Accept (Median & 90th Percentile)**:\
  Time from list display to acceptance.
  - **Formula**: Time to Accept = Timestamp of acceptance - Timestamp when list was shown
  - **Goal**: Lower or unchanged.

### Informative Metrics

- **Median Position of Accepted Job Requests**:
  - **Goal**: Lower.
- **Acceptance Rate at Selected Order**:
  - **Formula**: Acceptance Rate at position i = (Number of accepts at position i) / (Total number of accepts)
  - **Goal**: Higher in top ranks.

## Hypothesis

**If we implement the new ranking algorithm, the Top 3 Acceptance Rate will increase because suppliers will see the most suitable job requests first.**

## Data Generation

Synthetic data is generated for suppliers in both groups:

- Each supplier views 5–15 job requests.
- Acceptance depends on suitability score and list position.
- Events tracked: `open` (job viewed) and `accept` (job accepted).

## Simulation Code

- Executed in the `ab-testing-simulation.ipynb` notebook.
- Simulates 1056 suppliers per group.
- Data stored in a pandas DataFrame for analysis.

## Results and Analysis

- **Target Metric**: Treatment significantly improved Top-K Acceptance Rate (p &lt; 0.05).
- **Guardrail Metrics**:
  - **Overall Acceptance Rate**: Increased (positive).
  - **Time to Accept**: Remained stable (neutral).
- **Multiple Testing Note**:
  - Eventhough we did statistical tests for the guardrial metrics, no statistical adjustment (e.g., Bonferroni correction) is applied to the primary metric, as it serves as the main decision-making criterion.

## Conclusion

- **Key Findings**:
  - The new algorithm significantly improved the **Top-K Acceptance Rate**.
  - **Overall Acceptance Rate** increased, enhancing supplier engagement.
  - **Time to Accept** remained stable, preserving user experience.
- **Practical Significance**:
  - Faster job acceptance improves supplier efficiency.
  - Increased engagement may boost platform revenue.
  - Stable Time to Accept ensures a seamless experience.

## Recommendation

- **Action**: Launch the new ranking algorithm platform-wide.
- **Expected Benefits**:
  - Improved recommendation relevance and faster job acceptance.
  - Potential 5–10% increase in monthly completed jobs.
- **Next Steps**:
  - Monitor supplier feedback post-launch via dashboards.
  - Periodically evaluate acceptance rates and user experience metrics.