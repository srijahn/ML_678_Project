# Ranking vs Calibration for Month-6 Credit Default Prediction
ES 678 course project. Compares logistic regression, random forest and XGBoost
on the UCI "Default of Credit Card Clients" data (ID 350), with Platt and
isotonic calibration, a sensitivity study, a subgroup audit and a cost-threshold analysis.

## Files
- `Project_Code_ML678.py`: main results (models, calibration, bootstrap CIs, sensitivity, subgroups, cost)
- `results/`: output CSVs and `reliability.png`
- `ML_678_Report.pdf` / `.tex`: the paper

## Data
Download `default of credit card clients.xls` from
https://archive.ics.uci.edu/dataset/350/default+of+credit+card+clients

## How to run
pip install pandas numpy scikit-learn xgboost matplotlib xlrd openpyxl
python Project_Code_ML678.py "default of credit card clients.xls" 2

## Settings used
- Split: stratified 70/15/15, seeds 0 and 1
- Tuning: randomized search, 4 configurations per model (2 in the sensitivity study), 5-fold CV on the training set
- RF and XGBoost: 100 trees; XGBoost run with `device="cuda"` (T4 GPU in Colab)
- Sensitivity, subgroup and cost analyses: seed 0 only; training fractions 25% and 100%

## AI-use disclosure
I used Claude (Anthropic) to help draft the experiment code and the paper text.
I ran all experiments myself and checked the reported numbers against the output files.

## Citations
- Data: UCI Machine Learning Repository, "Default of Credit Card Clients" (ID 350).
  I-C. Yeh and C-H. Lien, Expert Systems with Applications 36(2):2473-2480, 2009.
- Libraries: scikit-learn (Pedregosa et al., JMLR 2011), XGBoost (Chen and Guestrin, KDD 2016),
  pandas, NumPy, matplotlib.
- Methods: Platt scaling (Platt, 1999); isotonic regression calibration
  (Niculescu-Mizil and Caruana, ICML 2005); ECE (Guo et al., ICML 2017).
- No external code was copied; the pipeline was written for this project with AI assistance.

## Notes
- Calibrators are fit on the validation set; the test set is not used for tuning or calibration.
- GPU and CPU XGBoost runs can differ in the last decimals.
- AI use: Claude was used to help draft code and paper text 
