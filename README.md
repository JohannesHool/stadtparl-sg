# STADTPARL-SG
This is a repository that contains NLP tools for downloading pdf files from the Ratsinformationssystem (RIS) of the city St. Gallen and extract and analyze their content.

The links to the files come from the OGD portal of the city of St. Gallen [daten.stadt.sg.ch](daten.stadt.sg.ch). For the text extraction OCR (**O**ptical **C**haracter **R**ecognition) is used, the text clustering is done with BERTopic.

The repository contains the following notebooks:

## 00_download.ipynb
This notebook downloads the dataset `traktandierte-geschaefte-sitzungen-stadtparlament-stgallen` from daten.stadt.sg.ch, filters it and uses the remaining rows to download the pdf files. The notebook produces the following output:
> 1. **data/source_table.csv** a semicolon separated csv containing the dataset *traktandierte-geschaefte-sitzungen-stadtparlament-stgallen* and an additional column called *local_file_path* with the path to the downloaded pdf files.
> 2. **data/pdfs** a folder that contains the pdf files. The names of the pdfs are generated using the date (sitzungsdatum) and the agenda item number (traktandennummer).

## 01_extract_text.ipynb
This notebook extracts the text from the pdfs using OCR and saves them to txt files. It produces the following output:
> 3. **data/texts** a folder containing the text files. The text files have the name of the corresponding pdf file.

## 02_topic_modelling.ipynb
This notebook reads all text from the txt files and uses BERTopic to produce a first topic clustering. While reading the txt files the text is cleansed in a rudimentary fashion. No hyperparameter tuning was conducted. The resulting clusters are generated using the default settings of the BERTopic library. The notebook produces the following output:
> 4. **data/clustering** the folder containing the output of the topic clustering.
> 5. **data/clustering/skipped_text.txt** a text file that contains all text that was skipped while reading. This is the output of the initial text cleansing as the pdf files contain headers that don't contain text relevant for the clustering.
> 6. **data/clustering/text_chunks.csv** a tab-separated csv file containing the text used for the clustering. The text is split up into manageable chunks and provided with an id for the original pdf file and a document level id for the chunk.
> 7. **data/clustering/text_chunks_topics.csv** a tab-separated csv file containing the text used for the clustering. Together with the class generated during the clustering.
> 8. **data/clustering/text_topics.csv** a tab-separated csv file containing one row per pdf file together will all topics that were attributed to this file during clustering.
> 9. **data/clustering/topics_with_keywords.csv** and **data/clustering/topics_with_keywords_and_keywordimportance.csv** two tab-separated csv files that list all topic ids generated during the clustering and the keywords describing those topic clusters.
> 10. **data/topic_visualization_map.html** a html document showing the topic clusters on two dimensions with hover information (tooltipps).
> 11. **data/topic_visualization_hierarchical.html** a html document showing the hierarchy of topics that could be achieved using topic reduction.

