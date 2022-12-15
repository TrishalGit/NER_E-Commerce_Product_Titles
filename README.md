# NER_E-Commerce_Product_Titles
## Setup
 - Please use Google Collab for executing the code 'ModelCode/BILSTM_Code.ipynb'.
 - Other code files can be executed in Jupyter Notebook.
 - Check the file paths in the code before execution or if you face errors. All the required files are placed in Dataset Folder.
## Execution of Code
 - Copy the Dataset Folder to your drive.
 - Upload 'ModelCode/BILSTM_Code.ipynb' to you Google Collab account.
 - Enable 'GPU' access on Collab.
 - Click 'Runtime' -> 'Run all'.
 - You will get a prompt to connect to drive. This is to connect with dataset files. Accept and allow the permission.
 - Code runs for 50 Epochs approximately takes 45 min to 1 hr for a complete execution.
 - The prediction results will be stored in a file names 'result\<Type\>.tsv' file.
## Evaluation F1-Score
 - Execute 'ModelCode/F1ScoreCalculator.ipynb'. To get the F1 score on the actual labels 'labels\<Type\>.csv' and predicted labels 'result\<Type\>.tsv'.
## Additional Steps for Glove Data
 - We have only added our custom built word embedding vectors file 'Custom.100d.txt' for current code.
### Pre-Built Glove Data
 - Download Pre-Trained dataset zip file from [Glove Dataset](https://nlp.stanford.edu/data/glove.6B.zip).
 - Unzip the folder.
 - Copy the 'glove.6B.100d.txt' file to 'Dataset' folder and replace the path in 'ModelCode/BILSTM_Code.ipynb' file.
### Generate custom Glove Data
 - Clone the Glove github repository in local [Github](https://github.com/stanfordnlp/GloVe).
 - Need GNU compiler to successfully execute 'make' command and build the code. Our system version used = GNU Make 3.81.
 - Go inside the GloVe folder and update 'Makefile' on line #11 replace '-march=native' with '-mcpu=lightning'. This is specific to running Glove code successfully on Mac M2 chip.
 - Update the 'demo.sh' file line #27 and change VECTOR_SIZE to 100.
 - Need to copy add text8 file that contains words and sentences related to our custom data otherwise it automatically downloads sample data online and builds the vectors based on that data.
 - We generated our text8 file through executing the code 'GloveTextGenerator.ipynb' on our dataset. The code and text8 file is present in 'DatasetProcessors' and 'DatasetProcessors/Data' folders.
 - Inside the 'Glove' directory. Run 'make' and then './demo.sh'. This will generate custom 'vectors.txt' file for the word embeddings.
## Structure of Dataset Files (Dataset Folder)
 - eng.train\<Type\> - This file is the training file consisting of words and tags for product titles in BIO format.
 - labels\<Type\>.csv - This file contains the actual labels assigned for the test product titles.
 - result\<Type\>.tsv - This file is generated as an output from the code and contains the predictions of entities on test set.
 - tags\<Type\>.csv - As the code doesn't consider spaces in the Tags. We created a mapping of original tags with the space removed tags. Used by the code.
 - testTitles\<Type\>.csv - This file has the test titles with record number.
 - Custom.100d.txt - Custom word embeddings file generated by Glove. Can be replaced with original pre-trained Glove 6B dataset. We are not adding the original file because of space constraints.
## Additional Data Processing Files (DatasetProcessors folder)
### Note: There might be miss-match in the code paths and lines. Just keeping this as a reference to the effort placed for generating the amazon dataset. For any issues please contact the contributors @Trishal gayam, @Hirthik Mathavan, @Pavan Boppudi, @Awani Kendurkar, @Richa Parte.
#### GloveTextGenerator.ipynb
 - This code generates the file ('text8') consisting of all the product title sentences appended to each other with space separation.
#### DataFormatter.ipynb
 - This code generates the training file (BIO) format and tags mapping for training data csv file.
#### Amazon Filter Extractor.ipynb
 - This file is used to pull the initial filter url from amazon.com.
 - Please use your own cookie (information can be accessed through postman) to get the data from amazon.com.
 - All the result files are placed in 'Filters' folder.
#### FilterToCategoryMapper.ipynb
 - This file to extract main filters and their keyword mapping file in csv format to represent a dictionary. The resultant file is used to map entity names for each category in product titles.
 - The file 'MainFilters.csv' in 'Data' folder shows the result of the above file where we additionally added few more keywords for each category manually and increased the number of categories.
#### ProductTitleExtractor.ipynb
 - This file is used to get all the product titles information based on filters applied from Amazon.
 - The code had to be run for multiple days to collect around 88k product titles.
 - Generates data files with product titles per filter in csv format. Data present in 'AmazonData' folder.
#### AmazonDatasetCreator.ipynb
 - This file is used to filter out unique product titles and map the entities with the product titles to generate separate files for 3 datasets used in the experimentation. Also has some code to generate 'text8' file used by glove.
#### TrainTestValidationSplit.ipynb
 - This code is used to generate separate train test and validation split for each dataset.
#### We might be missing some other code files used as building Amazon dataset was a long process. Feel free to reach out to our team for any help.

## Experimenting on BILSTM Model Code
 - Major code reference was used from this [repository](https://github.com/jayavardhanr/End-to-end-Sequence-Labeling-via-Bi-directional-LSTM-CNNs-CRF-Tutorial)
 - The above repository got reference from these 2 parent repositories [link1](https://github.com/ZhixiuYe/NER-pytorch) and [link2](https://github.com/glample/tagger).
 - The code is based on a research paper reference added to the report.
### Additional work and experimentation our group performed on the code
 - We had to modify the output generation code and processing the tag information for that code to match for our requirements.
 - We experimented with changing the number of layers in the LSTM and reducing the vector size of CNN. But, didn't find any sugnificant change.
 - We experimented with adding validation set split from our training set. But, the results were lower than training on our complete train set. This may be due to less amount of data present.
 - Experimentation with custom GloVe word embedding and dropout layer are explained in the report.
 - The code has given flexibility in understanding the methods more clearly and modify rather than using a direct library function.
