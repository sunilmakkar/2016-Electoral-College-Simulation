# 2016 Presidential Election Monte Carlo Simulator

A data engineering and statistical analysis project that explores "what-if" scenarios for the 2016 US Presidential Election using distributed computing on Databricks. This simulation demonstrates how small changes in swing state outcomes could have dramatically altered Electoral College results.

## Overview

This project implements a Monte Carlo simulation framework to analyze electoral volatility by randomly flipping swing state outcomes across 1,000+ iterations. Built using Apache Spark and Delta Lake, it showcases modern data engineering practices including medallion architecture (Bronze/Silver/Gold layers) and distributed data processing.

## Business Problem

Electoral outcomes often hinge on narrow margins in a handful of swing states. This simulation quantifies electoral volatility by answering: **"How would different swing state outcomes have changed the 2016 election?"**

Understanding this volatility has applications in:
- Political forecasting and campaign strategy
- Risk analysis for policy-dependent investments
- Understanding the fragility of electoral outcomes

## Technical Architecture

### Data Pipeline
1. **Bronze Layer**: Raw election data ingestion (1976-2020 presidential results)
2. **Silver Layer**: Cleaned, aggregated state-level vote totals with calculated vote shares
3. **Gold Layer**: Analytical tables with win probabilities and simulation results

### Core Components
- **Data Processing**: PySpark for distributed computation of 1,000+ simulations
- **Storage**: Delta Lake for ACID transactions and time travel capabilities
- **Simulation Engine**: Monte Carlo method with configurable flip probabilities
- **Electoral College Logic**: Winner-take-all state system with 270-vote threshold
- **Visualization**: Matplotlib for scenario comparison and distribution analysis

## Methodology

### Simulation Process
1. Load and clean historical election data at state and candidate level
2. Map all 50 states + DC to 2016 Electoral College vote allocations (538 total)
3. Define swing states based on historical competitiveness
4. For each simulation iteration:
   - Randomly flip swing states based on configurable probability
   - Recalculate state winners using adjusted vote totals
   - Aggregate Electoral College votes per candidate
   - Determine overall winner (270+ votes required)
5. Aggregate results across all simulations to calculate win probabilities

### Scenarios Analyzed
- **Base Scenario**: 4 swing states (FL, PA, MI, WI) with 50% flip probability
- **Aggressive Scenario**: Same 4 states with 80% flip probability
- **Extended Scenario**: 8 swing states with 50% flip probability

## Key Findings

| Scenario | Candidate A Win % | Candidate B Win % | Avg Electoral Votes A | Avg Electoral Votes B |
|----------|------------------|-------------------|----------------------|----------------------|
| Base (4 states, 50% flip) | 51.4% | 48.6% | 284 | 287 |
| Aggressive (4 states, 80% flip) | 9.7% | 90.3% | 279 | 296 |
| Extended (8 states, 50% flip) | 22.2% | 77.8% | 284 | 299 |

### Insights
- The election outcome was highly sensitive to small changes—essentially a coin flip with adjusted swing states
- Flipping just 4 key swing states produced near 50/50 outcomes in base scenario
- Higher flip probability (80%) dramatically shifted win probability, revealing the narrow margin of victory
- Adding more swing states increased outcome volatility, demonstrating the Electoral College's vulnerability to regional shifts

## Tech Stack

**Languages & Frameworks**
- Python 3.12
- PySpark (Distributed Computing)
- SQL (Delta Lake queries)

**Data Engineering**
- Databricks Community Edition
- Delta Lake (ACID transactions, time travel)
- Apache Spark (distributed processing)

**Data Visualization**
- Matplotlib
- Pandas (aggregation for visualization)

**Architecture Pattern**
- Medallion Architecture (Bronze → Silver → Gold)

## Skills Demonstrated

- **Data Engineering**: ETL pipeline design, Delta Lake medallion architecture
- **Distributed Computing**: PySpark transformations and aggregations at scale
- **Statistical Analysis**: Monte Carlo simulation methodology, probability analysis
- **Data Modeling**: Electoral College logic implementation, vote aggregation
- **Cloud Computing**: Databricks platform, cluster management
- **Version Control**: Git workflow for notebooks
- **Data Visualization**: Multi-scenario comparison charts, distribution histograms

## Project Structure
```
├── Presidential_Elections.ipynb    # Main simulation notebook
└── README.md                        # Project documentation
```

## How to Run

### Prerequisites
- Databricks Community Edition account
- Election dataset (1976-2020 US Presidential results)

### Setup Instructions
1. Upload the notebook to Databricks workspace
2. Load election data as a Delta table
3. Run cells sequentially to execute the full pipeline
4. Modify flip probabilities and swing state lists in simulation cells to test different scenarios

### Customization
- Adjust `swing_states` list to test different state combinations
- Modify `flip_probability` parameter (0.0 to 1.0) to simulate different volatility levels
- Change `range(1000)` to increase/decrease simulation iterations

## Future Enhancements

- [ ] Extend to 2020 and 2024 elections for comparative analysis
- [ ] Add demographic weighting to flip probabilities based on population trends
- [ ] Implement parallel processing to scale to 10,000+ simulations
- [ ] Build interactive dashboard with real-time parameter adjustment
- [ ] Add confidence intervals and statistical significance testing
- [ ] Incorporate polling data to inform flip probabilities

## Contact

**Sunil Makkar**
- GitHub: [@sunilmakkar](https://github.com/sunilmakkar)
- Email: sunil.makkar97@gmail.com

## License

This project is available for educational and portfolio purposes.

---

*This project was built to demonstrate data engineering, distributed computing, and statistical analysis capabilities using real-world electoral data.*
