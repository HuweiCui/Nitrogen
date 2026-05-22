# Trade Matrix Iteration Code

This code iteratively adjusts the trade matrix for **products at each stage** of China's inter-provincial nitrogen flow model. The nitrogen flow model includes multiple stages (e.g., fertilizer production, agricultural cultivation, livestock consumption, food processing, etc.), each involving various products (e.g., wheat, maize, rice, soybean, pork, chicken, nitrogen fertilizer). For each product, the code takes as input an initial trade matrix, provincial consumption data, and official statistical production data (e.g., from the China Statistical Yearbook). It iteratively adjusts the trade matrix to minimize the discrepancy between the production derived from consumption and the trade matrix and the statistical production. The final output includes the iterated trade matrix and export data.

## System Requirements
- Operating System: Windows 11 (may also run on macOS or Linux but not tested)
- Python Version: 3.12.4
- Dependencies: pandas, numpy, openpyxl (for Excel I/O)
- Hardware: Standard personal computer (recommended RAM ≥8GB; demo run time <5 minutes)

## Installation Guide
1. Ensure Python 3.12.4 is installed. If not, download from [python.org](https://www.python.org/).
2. Install required packages. Open a terminal (Command Prompt or PowerShell) and run: `pip install pandas numpy openpyxl`
3. Expected installation time: ~1 minute (depends on network speed).

## Demo
### Steps to Run
1. Clone or download this repository to your local machine.
2. Prepare input data: In the `Trade matrix iteration` folder, ensure the following three Excel files exist: `Trade matrix.xlsx` (initial trade matrix), `Consumption.xlsx` (consumption data by province), `Statistics_production.xlsx` (official statistical production data by province).
3. Run the main script `Matrix_iteration.py`: `python Matrix_iteration.py`
4. The program iteratively adjusts the trade matrix and prints the maximum error at each iteration.

### Expected Output
- Console output: Maximum error percentage at each iteration until error <5% (adjustable) or maximum iterations reached.
- Two Excel files: `Trade matrix_after Iteration.xlsx` (iterated trade matrix) and `Export_after Iteration.xlsx` (iterated export amounts by province). Files are saved to `E:\China Nitrogen Cycle Data\Iterative Data` by default (you may change the output path in the code).

### Expected Run Time for Demo
On a standard Windows 11 computer (8GB RAM), each run completes in less than 5 minutes using the provided sample data.

## Instructions for Use (How to Run on Your Own Data)
1. Prepare your input data in the same format as the example files: `Trade matrix.xlsx` (32 rows, 34 columns; first 32 columns: inter-provincial transfer matrix; column 33: export amounts; column 34: export ratio); `Consumption.xlsx` (two columns: province name and consumption); `Statistics_production.xlsx` (two columns: province name and statistical production).
2. Modify the file paths in the code (`A_path`, `consumption_path`, `actual_production_path`) and the output path (`output_path`) to point to your data files.
3. Adjust iteration parameters if needed: `tolerance` (default 0.05 for 5% error), `max_iter` (default 20000).
4. Run the script. The program will output the iterated trade matrix, export amounts, and a production comparison table.
5. **For each product at each stage of the nitrogen flow model** (e.g., nitrogen fertilizer, wheat, maize, pork, poultry meat), prepare the corresponding input files and run the code separately for each product. Each run is independent, allowing control over the error of the trade matrix for each product.

## Notes
- The code assumes that province names in the consumption and production files follow the same order as in the trade matrix. A built-in cleaning function removes suffixes like "Province", "City", "Autonomous Region". Ensure your province names can be matched correctly.
- If your data includes Hong Kong, Macao, or Taiwan, adjust the province list accordingly (the original code is based on China's 31 provinces, excluding Hong Kong, Macao, Taiwan).
