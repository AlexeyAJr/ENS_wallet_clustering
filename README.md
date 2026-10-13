# ENS Wallet Clustering: Whales, Market Makers and the Crowd

Clustering of Ethereum Name Service (ENS) token wallets into **whales**, **market makers** and **the crowd** based on their transaction history.

## How it works

1. Load ENS transfer data (CSV) and clean it.
2. Compute each transaction's balance change in USD (`value * price`), negative for the sender and positive for the recipient.
3. Aggregate per wallet: transaction count, min, max, mean, median and std of balance change.
4. Normalize the transaction count and mean balance change.
5. Choose the number of clusters with the elbow method and run K-Means with 3 clusters.
6. Visualize the clusters (Matplotlib) and export results to Excel and a Sweetviz HTML report.

## Data

CSV with ENS token transfers. Required columns: `ts`, `from_address`, `to_address`, `value`, `price`.

## Usage

```bash
pip install pandas numpy matplotlib scikit-learn sweetviz openpyxl jupyter
jupyter notebook ens_cluster_matplotlib.ipynb
```

Place the CSV file in the project folder and run the notebook cells in order.

## Output

- `labeled_summary.xlsx` — per-wallet statistics with cluster labels
- `report.html` — Sweetviz report
- Scatter plot of clusters: number of balance changes vs. mean balance change

## Notes

K-Means cluster numbers are arbitrary, so identify which cluster is whales, market makers or the crowd from the plot after each run. Set `random_state` for reproducible results.
