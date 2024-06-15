# Multi-Touch Attribution Analysis for Optimizing Digital Marketing Strategies

## Overview

In today's complex digital landscape, consumers interact with multiple marketing channels before making a purchase. Understanding the contribution of each channel is crucial for optimizing marketing strategies and budget allocation. This project employs various attribution models—First Touch, Last Touch, Exponential Touch, and data-driven approaches using Markov Chains and Shapley Values—to analyze and enhance the effectiveness of different marketing channels. By leveraging these insights, businesses can make data-driven decisions to improve campaign performance, increase ROI, and enhance customer engagement.

## Key Attribution Models

### First Touch Attribution
Attributes the entire conversion to the first interaction channel.
- **Formula:** 
  \[
  \text{First Touch Attribution} = \frac{\text{Conversions from first touch}}{\text{Total conversions}} \times 100
  \]

### Last Touch Attribution
Attributes the entire conversion to the last interaction channel.
- **Formula:**
  \[
  \text{Last Touch Attribution} = \frac{\text{Conversions from last touch}}{\text{Total conversions}} \times 100
  \]

### Exponential Touch Attribution (Radioactive Touch)
Uses exponential decay to assign more credit to interactions closer to the conversion event.
- **Formula:**
  \[
  \text{Radioactive Touch Attribution} = \sum_{i=0}^{n-1} (\text{decay factor})^{(n-1-i)} \times \text{channel}_{i}
  \]

### Data-Driven Attribution using Markov Chains
Uses transition probabilities between channels to assess the impact of removing a channel from the customer journey.
- **Key Steps:**
  1. Create a transition matrix based on channel interactions.
  2. Calculate removal effects and normalize them.

### Data-Driven Attribution using Shapley Values
Uses game theory to fairly distribute the credit of a conversion among all contributing channels.
- **Key Steps:**
  1. Calculate the marginal contribution of each channel in all possible combinations.
  2. Average the contributions to determine the Shapley value.

## Results

### Tabulated Attribution Results

#### First Touch Attribution
| Channel         | Conversions | Percentage |
|-----------------|-------------|------------|
| Paid Search     | 176         | 17.6%      |
| Social Media    | 172         | 17.2%      |
| Direct          | 172         | 17.2%      |
| Affiliate       | 170         | 17.0%      |
| Organic Search  | 159         | 15.9%      |
| Email           | 151         | 15.1%      |

#### Last Touch Attribution
| Channel         | Conversions | Percentage |
|-----------------|-------------|------------|
| Social Media    | 173         | 17.3%      |
| Affiliate       | 172         | 17.2%      |
| Organic Search  | 166         | 16.6%      |
| Paid Search     | 166         | 16.6%      |
| Direct          | 164         | 16.4%      |
| Email           | 159         | 15.9%      |

#### Exponential Touch Attribution
| Channel         | Conversions | Percentage |
|-----------------|-------------|------------|
| Affiliate       | 272.375     | 16.99%     |
| Direct          | 268.937     | 16.78%     |
| Organic Search  | 267.812     | 16.71%     |
| Social Media    | 267.750     | 16.70%     |
| Paid Search     | 267.500     | 16.69%     |
| Email           | 258.625     | 16.13%     |

#### Data-Driven Attribution using Markov Chains
| Channel         | Conversions | Percentage |
|-----------------|-------------|------------|
| Organic Search  | 0.172618    | 17.26%     |
| Affiliate       | 0.171038    | 17.10%     |
| Direct          | 0.165582    | 16.56%     |
| Paid Search     | 0.164895    | 16.49%     |
| Email           | 0.164549    | 16.45%     |
| Social Media    | 0.161318    | 16.13%     |

#### Data-Driven Attribution using Shapley Values
| Channel         | Conversions | Percentage |
|-----------------|-------------|------------|
| Email           | 0.174191    | 17.42%     |
| Paid Search     | 0.171511    | 17.15%     |
| Affiliate       | 0.166770    | 16.68%     |
| Social Media    | 0.166254    | 16.63%     |
| Direct          | 0.164090    | 16.41%     |
| Organic Search  | 0.157184    | 15.72%     |

### Comparison of Percentage Differences
| Channel         | First Touch % | Last Touch % | Exponential Touch % | Markov Chain % | Shapley Values % | Max % - Min % Difference |
|-----------------|---------------|--------------|---------------------|----------------|------------------|--------------------------|
| Paid Search     | 17.6%         | 16.6%        | 16.69%              | 16.49%         | 17.15%           | 1.11%                    |
| Social Media    | 17.2%         | 17.3%        | 16.70%              | 16.13%         | 16.63%           | 1.17%                    |
| Direct          | 17.2%         | 16.4%        | 16.78%              | 16.56%         | 16.41%           | 0.80%                    |
| Affiliate       | 17.0%         | 17.2%        | 16.99%              | 17.10%         | 16.68%           | 0.52%                    |
| Organic Search  | 15.9%         | 16.6%        | 16.71%              | 17.26%         | 15.72%           | 1.54%                    |
| Email           | 15.1%         | 15.9%        | 16.13%              | 16.45%         | 17.42%           | 2.32%                    |

### Plots

#### Attribution Comparison
![Attribution Comparison](path_to_attribution_comparison_plot.png)

#### Budget Allocation A/B Test
![Budget Allocation A/B Test](path_to_ab_test_plot.png)

## Practical Applications

1. **Budget Allocation:** 
   - Reallocate marketing budgets based on the insights from attribution models to maximize impact.
   - Example Code:
     ```python
     initial_budget_allocation = {'Email': 10000, 'Social Media': 15000, 'Paid Search': 20000, 'Organic Search': 8000, 'Direct': 5000, 'Affiliate': 3000}
     total_budget = sum(initial_budget_allocation.values())
     shapley_values_percentage = sv_attribution['Percentage'] / 100
     new_budget_allocation = shapley_values_percentage * total_budget
     new_budget_allocation = new_budget_allocation.to_dict()
     print(new_budget_allocation)
     ```

2. **A/B Testing and Iteration:** 
   - Validate budget allocations through A/B tests and continuously optimize spend.
   - Example Code:
     ```python
     def simulate_performance(budget_allocation):
         np.random.seed(42)
         performance = {channel: np.random.poisson(lam=budget / 1000) for channel, budget in budget_allocation.items()}
         return performance
     
     control_performance = simulate_performance(test_groups['Control'])
     test_performance = simulate_performance(test_groups['Test'])
     total_control_conversions = sum(control_performance.values())
     total_test_conversions = sum(test_performance.values())
     conversion_lift = ((total_test_conversions - total_control_conversions) / total_control_conversions) * 100
     print(f"Conversion Lift: {conversion_lift:.2f}%")
     ```

3. **Campaign Optimization:** 
   - Use time-of-day analysis for peak engagement and customer journey insights to improve user experience.

## Future Directions

- **Continuous Optimization:** 
  - Regularly update models and conduct A/B tests to stay aligned with consumer behaviors.
  
- **Advanced Modeling:** 
  - Explore more sophisticated models for deeper insights.

## Conclusion

By leveraging multi-touch attribution analysis, businesses can make informed decisions that enhance marketing performance, boost customer engagement, and drive growth. This project demonstrates the value of a data-driven approach to understanding and optimizing the contributions of various marketing channels.
