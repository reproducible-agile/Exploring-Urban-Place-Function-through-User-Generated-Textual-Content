This study employs two datasets: OSM POIs and Wikipedia article summaries. The OSM dataset provides very short textual data in the form of tags, which essentially represent the category of what is located at that position. Wikipedia articles can vary quite substantially in their length and structure. Our analysis is limited to the summaries of geo-located Wikipedia pages, which are more homogenous while still providing key information about the represented object. 
We conduct a series of NLP techniques on the collected datasets and developed a methodological framework that can work to extract place functional information from them. The codes for data collection are given as seperate files.
We have first adopted the classic Topic Modelling approaches, running them individually on each datasets. This includes LDA (Blei et al., 2003) and BTM (Yan et al., 2013). The codes to run the classic approaches are added here. Then a neural Topic Modelling approach, BERTopic (Grootendorst, 2022) was applied seperately on each datasets. Codes for running BERTopic is also provided here. The ways to evaluate the performance of the Topic Models are provided within the codes. 
We also leveraged some LLMs in place functional topic label generation from Wikipedia datasets. The codes to run each of them are also provided here.
Lastly, depending upon the quality of the performance of each method, a combination of best-performing method was adopted on a combined dataset of OSM and Wiki and the final place function label are represented.

To run the different part of the analysis there are in total 7 Jupyter Notebook, 1 R Markdown and 4 python files which needs to run at different sequential order. The first two files to run are for data collection, which includes the kc_osm_data_collection.ipynb and kc_wiki_data_collection.ipynb. These two files need an input of the London borough boundary files to run. The boundary file is available at: https://geoportal.statistics.gov.uk/datasets/417d65831892486bb88002c2e23520c1_0/explore?location=52.042712%2C-1.350081%2C7.98. The notebook for Wikipedia data also needs an input of csv file of geotags Wikipedia article list using which the summaries of the respective Wikipedia articles are queried. The outputs of running these codes are the OSM data and Wikipedia data for the Case study area (i.e., Kensington and Chelsea) which are used as input in the subsequent code files. 

For the Topic Modeling Modelling approach using OSM data, the next few files are run. First, osm_kc_dbscan_lda_btm_new2.ipynb is run to create spatial clusters using DBSCAN. Second, the steps to run LDA modeling followed by function labelling and spatial distribution mapping of the output results are shown. The BTM is run using two different files. First the model is run in R (BTM.Rmd). The tag list created for each dbscan in the previous file (osm_kc_dbscan_lda_btm_new2) is added as an input here. The results of BTM model is further used to label functions using the file, osm_kc_dbscan_lda_btm_new2.ipynb. The BERTopic model is run using the file bertopic_osm_new.ipynb. This file was created in Google Colab. The input for this file is the extracted OSM POIs csv file (i.e., new_kc_osm.csv) and output is the functions returned by running BERTopic modelling. 

Similarly the Topic Modelling approach is run for Wikipedia data. First the LDA model is performed using file kc_wiki_summary_lda_btm_new2.ipynb. The BTM model is run in BTM.Rmd file and the results of BTM model are labelled and mapped in kc_wiki_summary_lda_btm_new2.ipynb file. The input for the first python file is the kc_wiki_with_summary.csv file obtained from kc_wiki data collection. The output is the result of modelling LDA and BTM. The BERTopic model is run on bertopic_wiki_summry_new.ipynb file. The code was run in google colab. The input file is the same as for the other two models (kc_wiki_with_summary.csv) . The output is the BERTopic functions from Wiki summary data.  

Next the wiki+osm_kc_new.ipynb file is run. It uses the osm data and wiki data collected together as an input. It returns the combined functions from running BTM on OSM and BERTopic on Wikipedia data.

Finally codes are provided to run the Large Language Models (LLMs). The files run for each models are as follows, 
1. Mistral-7B - codes wiki_llm_c45_4-12-1.py
2. Llama-3 - codes wiki_llm_c45_llama3-b.py
3. Llama-3.2 - codes wiki_llm_c45_llama3.2-b.py
4. Phi-mini - codes wiki_llm_phi_mini-1-b.py

Each of these codes are run in python in GPU-enabled device. The input for the files are the list of Wikipedia Article Summaries grouped by DBSCAN clusters formed in the kc_wiki_summary_lda_btm_new2.ipynb. The output for each of these files are the topic labels generated by the models. 

