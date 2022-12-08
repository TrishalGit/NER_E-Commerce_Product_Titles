# NER_E-Commerce_Product_Titles
## Setup
 - Please use Google Collab for executing the code 'BILSTM_Code.ipynb'.
 - Other code files can be executed in Jupyter Notebook.
 - Check the file paths in the code before execution or if you face errors. All the required files are placed in Dataset Folder.
## Execution of Code
 - Copy the Dataset Folder to your drive.
 - Upload 'BILSTM_Code.ipynb' to you Google Collab account.
 - Enable 'GPU' access on Collab.
 - Click 'Runtime' -> 'Run all'.
 - You will get a prompt to connect to drive. This is to connect with dataset files. Accept and allow the permission.
 - Code runs for 50 Epochs approximately takes 45 min to 1 hr for a complete execution.
 - The prediction results will be stored in a file names 'result\<Type\>.tsv' file.
## Evaluation F1-Score
 - Execute 'F1ScoreCalculator.ipynb'. To get the F1 score on the actual labels 'labels\<Type\>.csv' and predicted labels 'result\<Type\>.tsv'.
## Additional Steps for Glove Data
 - We have only added our custom built word embedding vectors file 'Custom.100d.txt' for current code.
### Pre-Built Glove Data
 - Download Pre-Trained dataset zip file from [Glove Dataset](https://nlp.stanford.edu/data/glove.6B.zip).
 - Unzip the folder.
 - Copy the 'glove.6B.100d.txt' file to 'Dataset' folder and replace the path in 'BILSTM_Code.ipynb' file.
### Generate custom Glove Data
 - Clone the Glove github repository in local [Github](https://github.com/stanfordnlp/GloVe).
 - Need GNU compiler to successfully execute 'make' command and build the code. Our system version used = GNU Make 3.81.
 - Go inside the GloVe folder and update 'Makefile' on line #11 replace '-march=native' with '-mcpu=lightning'. This is specific to running Glove code successfully on Mac M2 chip.
 - Update the 'demo.sh' file line #27 and change VECTOR_SIZE to 100.
 - Need to copy add text8 file that contains words and sentences related to our custom data otherwise it automatically downloads sample data online and builds the vectors based on that data.
 - We generated our text8 file through executing the code 'GloveTextGenerator.ipynb' on our dataset. The code and text8 file is present in 'DatasetProcessors' and 'DatasetProcessors/Data' folders.
 - Inside the 'Glove' directory. Run 'make' and then './demo.sh'. This will generate custom 'vectors.txt' file for the word embeddings.
