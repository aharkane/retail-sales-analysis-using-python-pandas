# Retail Sales Analysis Using Python-Pandas

## Project Overview

In this project i analyze transactional retail data from a company acquisition target. This project demonstrates enterprise-level exploratory data analysis (EDA), data wrangling, and business insights extraction from large-scale retail transaction datasets.

## Project Goals

- Perform exploratory data analysis on transactional retail data
- Implement data type optimization and memory efficiency improvements
- Conduct multi-dimensional business analysis across households, products, and categories
- Identify key customer segments and high-value product opportunities
- Extract actionable business insights for acquisition due diligence

## Technology Stack

| Component | Technology |
|-----------|-----------|
| **Language** | Python 3.x |
| **Data Processing** | Pandas, NumPy |
| **Data Visualization** | Matplotlib |
| **Dataset Size** | 2.1M+ transactions |
| **Data Types** | CSV, XLSX |
| **Notebook Environment** | Jupyter |

## Dataset Overview

**Transactions Dataset (transactions.csv):**
- **Records**: 2,146,311 transaction lines
- **Time Period**: Multi-week transaction history
- **Key Fields**: HouseholdKey, BasketID, Day, ProductID, Quantity, SalesValue, StoreID, RetailDisc, WeekNo, CouponDisc, CouponMatchDisc

**Product Dataset (product.csv):**
- Product master data with manufacturer, department, brand, and commodity information
- 84,138+ unique products

## Data Analysis Highlights

### Data Optimization & Cleaning

**Memory Efficiency Improvement**
- Optimized data types by casting columns to smallest appropriate types
- DAY: int64 → int8
- QUANTITY: int64 → int32  
- STOREID: int64 → int32
- WEEKNO: int64 → int8
- **Result**: Memory usage reduced from 180.1 MB to 135.1 MB (25% reduction)

**Data Quality Assessment**
- **Missing Data**: Zero missing values across all 11 columns
- **Unique Values**: 2,099 unique households, 84,138 unique products
- **Data Consistency**: All date and transaction fields validated

### Feature Engineering

**Discount Analysis**
- Calculated total discount across retail discount and coupon discount columns
- Derived percentage discount: (TotalDiscount / SalesValue).abs()
- Bounded discount percentages between 0 and 1
- Identified high-discount transactions for pricing strategy analysis


## Key Implementations

### Data Wrangling
```python
# Type casting for memory optimization
transactions = transactions.astype({
    'day': 'int8',
    'quantity': 'int32',
    'storeid': 'int32',
    'weekno': 'int8'
})

# Feature engineering
transactions = (transactions
    .assign(
        totaldiscount=transactions['retaildisc'] + transactions['coupondisc'],
        percentdiscount=lambda x: x['totaldiscount']/x['salesvalue']
    )
    .abs()
    .apply(lambda y: 1 if y > 1 else 0 if y < 0 else y)
    .drop(['retaildisc', 'coupondisc', 'couponmatchdisc'], axis=1)
)
```

### Exploratory Data Analysis
- Histogram distributions of household spending patterns
- Aggregation queries across multiple dimensions
- Top-N analysis with ranking and filtering
- Cross-tabulation and pivot table operations
- Groupby operations with multiple aggregation functions

## Repository Structure

```
├── data/
│   ├── Transactions.csv (main dataset - 52.7 MB)
│   └── Product.csv (product catalog - 6.4 MB)
├── Transactions-Analysis-using-Pandas.ipynb
└── README.md
```

## Key Accomplishments

✓ Processed 2.1M+ transaction records without memory issues  
✓ Achieved 25% memory reduction through intelligent type casting  
✓ Identified zero missing values (clean dataset)  
✓ Extracted multi-dimensional business insights  
✓ Segmented 2,099 customers into value tiers  
✓ Analyzed 84,138 products across multiple categories  
✓ Performed comprehensive EDA with visualization  
✓ Generated actionable recommendations for business stakeholders  

