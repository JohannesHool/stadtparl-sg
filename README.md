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

## 02_simple_analysis.ipynb
A notebook that generates simple plots that counts the number of Traktanden that contian one or multiple keywords over the years.
> 4. **data/output** a folder containing Plotly charts as html files

## 02_topic_modelling.ipynb
See commit [c40541c](https://github.com/JohannesHool/stadtparl-sg/commit/c40541c0e689d325874ee3b61cbeeb0ac268b490) ot see an exemplary notebook that does topic clustering using SBERT

