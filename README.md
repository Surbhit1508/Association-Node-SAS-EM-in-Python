# Bakery Market Basket Analysis

A comprehensive Python tool for analyzing bakery transaction data using market basket analysis techniques similar to the Association node in SAS Enterprise Miner.

## Overview

This application provides a complete solution for analyzing transaction data from a bakery, including:

1. **Market Basket Analysis** - Discover which products are frequently purchased together
2. **Profitability Analysis** - Identify your most profitable products
3. **Temporal Analysis** - Understand sales patterns by time of day and day of week
4. **Visual Analytics** - Generate insightful visualizations of all analyses

The core of this tool is the market basket analysis functionality, which implements the Apriori algorithm to find association rules between products. This is similar to the Association node in SAS Enterprise Miner, but with enhanced visualization capabilities.

## Features

- **Association Rule Mining**: Discover patterns in customer purchasing behavior using the Apriori algorithm
- **Comprehensive Metrics**: Calculate support, confidence, and lift to identify strong product associations
- **Network Visualization**: Visualize product relationships as a network graph
- **Heatmap Generation**: Create heatmaps to easily identify product pairs with strong associations
- **Business Intelligence Dashboard**: View profitability, temporal patterns, and product pairs in a single dashboard
- **Customizable Parameters**: Adjust support, confidence, and lift thresholds to fine-tune your analysis

## Requirements

- Python 3.8 or higher
- Required packages:
  - pandas
  - numpy
  - matplotlib
  - seaborn
  - mlxtend (for Apriori algorithm)
  - networkx (for network visualization)

You can install the required packages using pip:

```bash
pip install pandas numpy matplotlib seaborn mlxtend networkx openpyxl
```

Note: `openpyxl` is required for pandas to read Excel files.

## Data Format

The tool expects an Excel file with two sheets:
1. **Sheet 1**: Transaction data with columns for Transaction ID, Item, Date, and Time
2. **Sheet 2**: Cost data with columns for Item, Sale Price, and Our Cost

Example transaction data format:
| Transaction | Item         | Date       | Time     |
|-------------|--------------|------------|----------|
| 1           | Coffee       | 2023-01-01 | 08:30:00 |
| 1           | Croissant    | 2023-01-01 | 08:30:00 |
| 2           | Tea          | 2023-01-01 | 09:15:00 |
| 2           | Cookie       | 2023-01-01 | 09:15:00 |

Example cost data format:
| Item      | Sale Price | Our Cost |
|-----------|------------|----------|
| Coffee    | 3.50       | 1.20     |
| Croissant | 2.75       | 0.90     |
| Tea       | 2.50       | 0.75     |
| Cookie    | 1.50       | 0.45     |

## Usage

Basic usage:

```python
from bakery_analysis import run_bakery_analysis

# Run the analysis with default parameters
results = run_bakery_analysis(
    'BreadBasketT.xlsx',
    min_support=0.01,     # Minimum support threshold (1% of transactions)
    min_confidence=0.2,   # Minimum confidence (20% probability)
    min_lift=1.0          # Minimum lift (only positive associations)
)

# Print association rules summary
from bakery_analysis import print_association_summary
print_association_summary(results['association_rules'])
```

## Output

The tool generates several output files:

1. `bakery_analysis_dashboard.png` - A business intelligence dashboard with four key visualizations
2. `association_rules_network.png` - A network graph showing the relationships between products
3. `association_heatmap.png` - A heatmap showing the lift values between product pairs

Additionally, the `results` dictionary contains the following keys:

- `merged_data` - Preprocessed transaction data with cost information
- `item_pairs` - Simple count of item pairs frequency
- `profitability` - Profitability metrics for each product
- `hourly_sales` - Sales breakdown by hour of day
- `daily_sales` - Sales breakdown by day of week
- `items_by_hour` - Top items sold by hour
- `frequent_itemsets` - Frequent itemsets identified by the Apriori algorithm
- `association_rules` - Association rules with support, confidence, and lift metrics
- `visualization_file` - Path to the dashboard visualization file
- `network_visualization` - Path to the network visualization file
- `heatmap_visualization` - Path to the heatmap visualization file

## Understanding the Results

### Key Metrics

The association rules are evaluated using three key metrics:

1. **Support** - The percentage of transactions that contain both items. Higher values indicate more common combinations.
2. **Confidence** - The probability of buying the consequent given the antecedent. Higher values indicate stronger predictive power.
3. **Lift** - A measure of how much more likely items are to be purchased together than by chance. Values greater than 1 indicate positive association.

### Interpreting Visualizations

- **Network Graph**: 
  - Blue nodes are items that only appear as antecedents (they lead to other purchases)
  - Orange nodes are items that only appear as consequents (they are purchased as a result of other items)
  - Green nodes are items that appear as both antecedents and consequents
  - Edge thickness represents the strength of association (lift)

- **Heatmap**:
  - Intensity of color represents the lift value between item pairs
  - Higher lift values (darker blue) indicate stronger associations

## Customization

You can customize the analysis by adjusting the following parameters:

- `min_support`: Minimum percentage of transactions that must contain an itemset to be considered frequent
- `min_confidence`: Minimum probability threshold for association rules
- `min_lift`: Minimum lift value for association rules (values > 1 indicate positive association)

Example with stricter thresholds:

```python
results = run_bakery_analysis(
    'BreadBasketT.xlsx',
    min_support=0.02,     # Require items to appear in at least 2% of transactions
    min_confidence=0.3,   # Require at least 30% probability
    min_lift=1.5          # Require stronger positive association
)
```

## Comparison with SAS Enterprise Miner

This tool provides similar functionality to the Association node in SAS Enterprise Miner, with the following advantages:

- Open-source Python implementation (no SAS license required)
- Enhanced visualization capabilities, including network graphs and heatmaps
- Integration with profitability and temporal analysis
- Customizable parameters for fine-tuning the analysis
- Fully transparent algorithm implementation that can be modified as needed

## Future Enhancements

Potential future enhancements:

- Basket sequence analysis to understand the order of purchases
- Integration with customer demographic data for segmented analysis
- Implementation of additional association algorithms beyond Apriori
- Interactive dashboards using Plotly or Dash
- Automated recommendations based on discovered association rules

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- The Apriori algorithm implementation is based on the mlxtend library by Sebastian Raschka
- Visualization techniques are inspired by best practices in business intelligence and data visualization
