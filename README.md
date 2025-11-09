# Marketing Budget Optimization Using Linear and Mixed-Integer Programming

## Overview
This project presents a comprehensive and analytical approach to optimizing a company’s annual **$10 million marketing budget** using advanced optimization techniques. The goal is to determine how this budget should be allocated across ten different advertising platforms—such as TV, Print, Facebook, Instagram, LinkedIn, SEO, and AdWords—to achieve the **maximum possible Return on Investment (ROI)**. The project moves beyond intuition-based budgeting and builds a mathematical, highly interpretable framework using **Linear Programming (LP)**, **Mixed-Integer Programming (MIP)**, and **Dynamic Monthly Reinvestment**. In addition to identifying the optimal allocation, the project evaluates policy constraints, returns from different ROI structures, and operational considerations such as stability over multiple months. The result is a practical, data-driven guideline that senior leadership can use to improve marketing strategy and financial outcomes.

## Image
![Budget Optimization](images.jpeg)

## Problem Statement
Marketing budget decisions often suffer from limited visibility into platform-specific performance, leading to inefficient spending, arbitrary allocations, or over-dependence on a few familiar channels. In reality, marketing platforms have highly variable ROI curves: some exhibit **diminishing returns** (concave behavior), while others experience **irregular or non-concave returns**, where certain spending tiers produce sudden jumps or declines in ROI. Complicating this further, organizations typically enforce business rules such as maximum spending limits, proportional investment between traditional and digital media, and minimum spend thresholds required for meaningful impact. This project seeks to solve the central question: *How should a multi-million-dollar marketing budget be allocated across several platforms to maximize ROI while respecting financial, operational, and managerial constraints?*

## Exploratory Data Analysis (EDA)
The EDA phase focused on understanding the behavior of ROI across platforms and tiers. The first dataset revealed smooth diminishing returns, indicating concavity and suitability for Linear Programming. The second dataset exhibited non-concave, stepwise ROI curves, requiring a more complex MIP approach. Analysis showed that some platforms performed well at low spends but quickly became inefficient, while others yielded stronger returns only after crossing specific spending thresholds. Monthly ROI data revealed natural variability across the calendar year, with the strongest performance observed in **October** and the weakest in **February**. These behavioral patterns shaped all subsequent model design and decision-making logic.

## Modelling Approach
To fully capture the diversity in ROI structures, the project implemented multiple models, each tailored to specific properties of the data.

The first model used **Linear Programming** on the concave ROI dataset. Because this dataset exhibited diminishing returns, LP could efficiently determine the optimal fractional allocation across tiers. The model allocated the entire $10 million budget but did so in a highly concentrated manner, pushing spending toward the very best-performing platforms—mainly TV, Instagram, Email, and AdWords. This produced the highest return of **$0.5436 million** under concave assumptions.

The second model used **Mixed-Integer Programming** to address the non-concave ROI dataset. Here, binary decision variables were used to activate specific ROI tiers while ensuring adjacency through SOS2-style logic. This model captured the non-linear structure and provided a more balanced allocation across platforms such as Print, Facebook, AdWords, and LinkedIn. Although the return was lower (**$0.4528 million**) compared to the concave dataset, this model reflected realistic behavior when returns fluctuate across tiers.

An additional layer was introduced through **minimum spend activation constraints**, which ensured that a platform was only used if the investment exceeded a threshold that would produce meaningful results. This prevented the model from spreading small, ineffective amounts across too many platforms.

The most advanced stage of modeling extended this into a **12-month dynamic allocation framework**, where each month’s budget consisted of the base $10M plus **50% of the previous month’s return**. Because of this reinvestment mechanism, the monthly budgets ranged from $10M to $10.323M. Individual monthly models were solved independently, revealing seasonal allocation patterns and natural shifts in optimal platform selection.

## Evaluation and Results
Model evaluation compared returns across LP and MIP models, assessed robustness, and examined the influence of business constraints. The LP model performed best under concave assumptions, while the MIP model performed best under more realistic, non-concave conditions. Cross-scenario evaluations revealed large losses when applying the wrong model type to the wrong ROI structure. Constraints played a crucial role—especially the **$3M platform cap**, which emerged as the most consistently active and influential constraint, preventing excessive concentration in top-performing platforms.

The dynamic monthly optimization delivered a granular look at how budgets evolve over time. Monthly returns ranged from **$0.42M to $0.65M**, with the highest performance seen in October. However, analysis showed that the allocation plan was not operationally stable: there were **33 violations** where monthly changes in platform investment exceeded the allowed $1M threshold. This instability highlighted the trade-off between pure optimization and real-world feasibility. Additional stability constraints were proposed to address this concern.

## Business Insights and Implications
From a business standpoint, several important insights emerged:

1. **Concentrated spending is optimal**, not diversified spending. High-performing platforms consistently hit the spending cap, showing that in the absence of constraints, the model would continue allocating heavily to a select few.

2. **ROI model shape matters financially.** Using the wrong model (e.g., applying LP to non-concave data) can cost hundreds of thousands of dollars—highlighting the importance of matching modeling techniques to data behavior.

3. **Threshold effects are real.** If spending is below a platform’s minimum effective threshold, returns are negligible. This validates many real-world observations where marketing impact only materializes beyond a certain scale.

4. **Monthly variability requires controlled adjustments.** Without stability constraints, budget swings become operationally unrealistic. Real-world teams require smoother transitions than a mathematically optimal model alone would produce.

5. **Dynamic reinvestment amplifies long-term ROI.** Allowing budgets to grow through reinvestment creates compounding benefits across months.

These insights can help executives make more grounded budgeting decisions, reduce waste, and increase strategic clarity.

## Technology Used
This project was developed primarily in **Python**, using a combination of scientific, optimization, and visualization libraries. The **Gurobi Optimization Solver** was used to formulate and solve both linear and mixed-integer programming models. Additional tools included **Pandas** and **NumPy** for data manipulation, **Matplotlib** and **Seaborn** for data visualization, and **Jupyter Notebook** for interactive model development and iterative experimentation. The entire workflow reflects a blend of machine learning-style EDA with operations research techniques, making it both rigorously analytical and easy to interpret.

## Conclusion
This project demonstrates how analytical optimization models can transform marketing budget decisions by replacing intuition with data-driven strategy. Through LP, MIP, threshold-based activation, dynamic reinvestment, and stability checks, the project provides a complete framework for practical, high-impact budget optimization. The approach is flexible enough to be extended to other industries, larger budgets, or more complex constraints. It also offers leadership a transparent and explainable decision-making tool that directly aligns marketing spend with measurable financial outcomes. Ultimately, this project highlights the power of optimization in bridging the gap between mathematical modeling and real-world business strategy, giving decision-makers a robust roadmap for maximizing marketing ROI.

## Author
**Alisha Surabhi**  
MS Business Analytics – University of Texas at Austin  
