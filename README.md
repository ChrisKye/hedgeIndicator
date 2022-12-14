# Construction of HedgeIndicator.csv and HedgeIndicator_v2.csv

### HedgeIndicator (Version 1)
We downloaded all available 10-K and 10-Q filings from the SEC website using the sec-api Python package (https://pypi.org/project/sec-api). In order to construct the hedgeIndicator dataset, we downloaded the data in 3 parts: the positive matches (positives.py), the false positive matches (fpositivess.py), and all filings (master.py). The basic structure of the three scripts are the same; the most notable difference is the search terms used in the query. In order to ensure consistency in format across the outputs, we used the FullTextSearchApi (https://sec-api.io/docs/full-text-search-api) for all queries, which returns filings from 2000-01-01 up to present day. The list of query strings for positives and false positives can be found in the data folder. After the three datasets were downloaded, they were merged into hedgeIndicator.csv.

### HedgeIndicator (Version 2)
We repeated the process for a new set of gvkeys and CIK's. We downloaded filings for all firms in updated_keys.csv that were not already included in the original hedgeIndicator.csv. The queries were then merged through the same process described above. Finally, we extracted entries from the original hedgeIndicator.csv that were included in the new list (updated_keys.csv), then merged the two datasets together. All files relevant to v2 are labelled with the suffix "_v2".

### Code
*positives.py*: this code downloads all filings that include a string match in positives.txt  
*fpositivess.py*: this code downloads all filings that include a string match in fpositives.txt  
*master.py*: this code downloads all filings of each firm, if they exist.  
*merge.py*: this code performs final cleaning steps and merges positives.csv, fpositives.csv, master_v3.csv into hedgeIndicator.csv  
*text_editing.ipynb*:  
In order to circumvent the max. character count of each query specified by sec-api, false positive matches were downloaded in 3 separate queries. text_editing.ipynb splits the list of false positive query strings and formats each into non-delimited text files that can be read in as Python strings.

### Data
_positive.txt_: list of positive match strings  
_f_positive.txt_: list of false positive match strings  
_f_positive_clean_1.txt_: first false positive query string  
_f_positive_clean_2.txt_:	first false positive query string  
_f_positive_clean_3.txt_:	first false positive query string  
  
_gvkey_list.dta_: list of gvkeys used to perform searches for hedgeIndicator.csv  
_index.csv_: reference table to map gvkeys to CIK's for hedgeIndicator.csv  
_positive.csv_: table of positive matches  
_fpositive.csv_: table of false positive matches  
_master.csv_: table of all company filings  
_hedgeIndicator.csv_: final hedge indicator 
  
_updated_keys.csv_: reference table used for gvkey-CIK pairs in v2  
_positive_v2.csv_: table of positive matches in v2  
_fpositive_v2.csv_: table of false positive matches in v2  
_master_v2.csv_: table of all company filings in v2  
_hedgeIndicator_v2.csv_: final hedge indicator in v2  
  
_error_CIK.csv_:   
Due to the high volume of queries, the API generated some random errors in querying that resulted in inconsistent return values (i.e. missing filings). This file contains a list of CIK's with known errors.

