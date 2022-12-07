# NER_E-Commerce_Product_Titles
## Setup
 - Please use Google Collab for executing the code 'BILSTM_Code.ipynb'.
 - Other code files can be executed in Jupyter Notebook.
 - Check the file paths in the code before execution or if you face errors. All the required files are placed in Dataset Folder.
## Execution of Code
 - Copy the Dataset Folder to your drive.
 - Upload 'BILSTM_Code.ipynb' to you Google Collab account.
 - Enable 'GPU' access on Collab.
 - CLick 'Runtime' -> 'Run all'.
 - You will get a prompt to connect to drive. This is to connect with dataset files. Accept and allow the permission.
 - Code runs for 50 Epochs approximately takes 45 min to 1 hr for a complete execution.
 - The prediction results will be stored in a file names 'result<Type>.tsv' file.
## Evaluation F1-Score
 - Execute 'F1ScoreCalculator.ipynb'. To get the F1 score on the actual labels 'labels<Type>.csv' and predicted labels 'result<Type>.tsv'.
## Additional Steps for Glove Data
 - We have only added our custom built word embedding vectors file 'Custom.100d.txt' for current code.
### Pre-Built Glove Data
 - Download
