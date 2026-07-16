# TheLook Ecommerce Propensity Matching

This project analyses whether Email acquisition affects customer revenue using Propensity Score Matching.

## Setup

1. Create and activate a virtual environment.
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Open the notebook and run the cells in order.

## Project structure

- `data/` contains the CSV datasets used by the analysis.
- `notebooks/` is reserved for notebook files.
- `src/` can be used for reusable Python modules later.

## Project notes

- Keep one Python environment for the notebook to avoid package conflicts.
- The notebook expects the CSV files in the `data/` folder.
- If you add more analysis steps, move reusable logic into `src/` to keep the notebook cleaner.
