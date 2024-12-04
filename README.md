# Detailed Operation Steps

## 1.1 Data Sources

### 1.1.1 CiteSpace 6.2 R4 Analysis

The data source includes the Web of Science database. The study period ranges from January 1, 2004, to January 1, 2024, using a keyword search method. The search keywords are the English terms “internal fixation” and “materials.” Articles were screened based on predefined inclusion and exclusion criteria, and duplicate entries were removed. This process resulted in a total of 2,344 English articles.

### 1.1.2 VOSviewer Analysis

The Web of Science database was used as the data source. The search terms were “internal fixation” and “materials,” with English as the publication language. Articles were screened based on established inclusion and exclusion criteria, and duplicate articles were excluded. A random selection of recent relevant articles resulted in a total of 2,344 articles.

## 1.2 Inclusion and Exclusion Criteria

### 1.2.1Inclusion Criteria:

Included document types: articles and research papers.

Excluded document types: duplicate articles, conference abstracts, press releases, informational pieces, and reviews.

### 1.2.2 Relevance to the Topic:

Studies related to the themes of “internal fixation” and “materials,” covering various material types, fixation device performance, biocompatibility, and other related topics.

## 1.3 Data Processing and Analysis

The retrieved Chinese literature was screened according to the inclusion and exclusion criteria, exported in Refworks format, and renamed as “download_01-download_03.” CiteSpace 6.2 R4 software was then used to visualize authors, institutions, and keywords, generating visual analysis graphs to further describe the research status, hotspots, and trends in internal fixation materials.

English literature retrieved from the Web of Science database was screened according to the inclusion and exclusion criteria. The relevant articles were exported in RIS format and renamed “download_04.” Articles exported in Plain Text File format were renamed as “download_05-download_12.” CiteSpace 6.2 R4 and VOSviewer software were used to conduct visual analyses of authors, institutions, and keywords, generating visual analysis graphs to further describe the research status, hotspots, and trends in internal fixation materials.

## 1.4 Analysis Parameter Settings

### 1.4.1 CiteSpace 6.2 R4 Analysis Settings

An analysis target folder needs to be created, containing four subfolders named “input,” “output,” “data,” and “project.” The processed exported data should be placed in the “input” folder. Use the CiteSpace 6.2 R4 data key for data format conversion, selecting an appropriate literature data source such as Web of Science. Once the data conversion is complete, move the converted files from the “output” folder to the “data” folder and create a new working dataset. On the new page, name the dataset, set the default data source to WoS, and save it. Set the interval for literature data, and choose options like “author” and “keyword” for visualization analysis. After completing the analysis, click on the visualization map options and highlight keywords as needed.

### 1.4.2 VOSviewer Analysis

Create a target analysis folder and place the exported database data within it. Click “Create” to set parameters, selecting the option “Create a map based on text data.” Choose the database data source and open the corresponding folder by selecting the appropriate database button. Select the “Title” and “Abstract” fields, choose the “Binary Counting” option, and adjust the frequency and interval of keyword display according to personal preference. Finally, generate a keyword clustering map. To obtain the final visual density map, select the “Density Visualization” option.

## 1.5 Open Source Code Structure

```
├── data/          # Raw data files

│  ├── savedrecs1.txt    # Dataset 1

│  ├── savedrecs2.txt    # Dataset 2

│  ├── savedrecs3.txt    # Dataset 3

├── scripts/         # Python scripts

│  ├── preprocess_data.py  # Data preprocessing script

├── docs/          # User documentation

│  ├── README.md      # Project overview

│  ├── VOSviewer_guide.md  # VOSviewer user guide

│  ├── CiteSpace_guide.md  # CiteSpace user guide

└── LICENSE         # Open source license
```

```shell
python preprocess_data.py --input data/savedrecs1.txt --output data/processed_data.csv
```

```python
import pandas as pd

import argparse

def preprocess_data(input_file, output_file):

  \# Read txt data

  data = pd.read_csv(input_file, delimiter='\t', encoding='utf-8', error_bad_lines=False)

  \# Extract keywords and titles

  keywords = data['Keywords'].dropna()

  titles = data['Title'].dropna() 

  \# Count keyword frequencies

  keyword_counts = keywords.str.split(';').explode().value_counts()

  \# Save results

  keyword_counts.to_csv(output_file, index=True, header=['Keyword', 'Frequency'])

  print(f"Processed data saved to {output_file}")

if __name__ == "__main__":

  parser = argparse.ArgumentParser(description="Preprocess bibliometric data")

  parser.add_argument('--input', required=True, help="Input file path")

  parser.add_argument('--output', required=True, help="Output file path")

  args = parser.parse_args()

 preprocess_data(args.input, args.output)
```





## 1.6 VOSviewer Metrics Output

VOSviewer focuses on the construction and analysis of network maps, and the main metrics it outputs are as follows:

1. Node Metrics

Size:

The size of a node reflects its weight or importance, such as the frequency of occurrence of a particular keyword or the number of publications by an author.

Color:

Colors represent clusters, which are groups divided based on co-occurrence relationships or coupling strength.

2.  Edge Weight (Links)

Link Strength:

Indicates the strength of the relationship between two nodes, such as the number of times two keywords appear together in the literature.

Total Link Strength:

Represents the total strength of connections between one node and all other nodes.

3. Output Files

Map File: Contains data on the map, including nodes, edges, and cluster information.

Network File: Saves the network structure, including node weights and link strengths.

How to Retrieve These Metrics from VOSviewer?

In the map interface, right-click on a node to view specific values (e.g., keyword frequency, link strength).

Use the "Save as" function to export data files (e.g., *.map or *.txt).

Analyze node metrics and relationships further using the software's generated tables or matrices.

## 1.7 CiteSpace Metrics Output

CiteSpace focuses on constructing scientific knowledge maps based on temporal dimensions, with metrics leaning more toward bibliometrics. The main metrics include:

1. Betweenness Centrality

Reflects the role of a node in connecting different sub-networks. A higher value indicates that the node serves as a significant bridge in the network.

Often used to identify key authors, institutions, or keywords in a field.

2. Burstness

Used to identify research hotspots or keywords with significant growth over a particular period.

CiteSpace detects the "burst strength" (Strength) and duration (Start-End) of certain keywords or topics using algorithms.

3. Cluster Labels

Generated based on clustering analysis of keywords or citation content, providing thematic labels for each cluster.

Typically created automatically by the software's algorithms.

4. Output Files

Visual Maps: Generated image files displaying the network of nodes and links.

Analysis Report: Contains lists of burst keywords, centrality rankings, and other metrics.

How to Retrieve These Metrics from CiteSpace?

After analysis, check the "Analysis Report" file:

Includes burst keywords and their strengths, centrality rankings, etc.

Use the "Export" function to save visual maps as images or .gexf files for further analysis or presentation.

## 1.8 Process for Generating These Metrics

1.  Data Import

Import Web of Science data files (savedrecs*.txt) and select the target node type (e.g., keywords, authors, institutions).

2. Set Analysis Parameters

Adjust the analysis range (time windows, node filtering thresholds, etc.).

In VOSviewer, choose co-occurrence analysis or co-citation analysis.

In CiteSpace, choose time slicing and burst detection.

3. Run Analysis and Output Results

VOSviewer:

After generating the network map, click on nodes to view detailed metrics.

Export maps and node data files for subsequent use.

CiteSpace:

After generating the knowledge map, save the analysis report and image files.

View key metrics in the report.

 

![Figure 14 Timeline Visualization of Research Keywords in Literature](https://github.com/user-attachments/assets/fe8c4c14-ab3b-4412-a466-7cc720f6e500)
![Figure 13 Visual Map of Research Keywords in Literature](https://github.com/user-attachments/assets/bfda9db7-6c6d-44f5-9f01-4905567cb245)
![Figure 12 Temporal Visualization of Keywords in Literature](https://github.com/user-attachments/assets/52738451-1f44-4cce-aea8-b1d8c54c90e7)
![Figure 11 Visualization of Keyword Clustering Analysis](https://github.com/user-attachments/assets/479739e9-48df-4dad-96e9-cd61d6530603)
![Figure 10 Visualization of Keyword Clustering Analysis](https://github.com/user-attachments/assets/8991ae1b-6472-4ddb-afe4-24cf81a22c61)
![Figure 9 Keyword Density View](https://github.com/user-attachments/assets/2544bf2e-5832-4d01-9cbb-eed95be384c3)
![Figure 8 Keyword Label View](https://github.com/user-attachments/assets/759652f4-209e-4f04-9d7c-a5a4105c95c4)
![Figure 7 Research Theme Clustering Network](https://github.com/user-attachments/assets/b2132fd0-570e-4124-a911-f82723ca64b3)
![Figure 6 Citation Burst Map of Authors](https://github.com/user-attachments/assets/c8657289-c988-40e8-b1b8-3b83b0e8b4fc)
![Figure 5 Keyword Significance Map for Major Countries Worldwide](https://github.com/user-attachments/assets/d498ff75-a688-480c-9eb7-88643c0e8fc4)
![Figure 4 Global Distribution of Authors, Countries, and Institutions](https://github.com/user-attachments/assets/33ae917f-45c6-4eda-bd44-f0d30bd34d41)
![Figure 3 Line Chart of Publication Growth](https://github.com/user-attachments/assets/6331d519-63c3-4656-9379-086468fdb503)
![Figure 2 Annual Number of Publications (2004–2024)](https://github.com/user-attachments/assets/3496179b-c93a-437f-a235-c1be26704113)
![Figure 1 Literature Screening Process](https://github.com/user-attachments/assets/43733aaa-c1bc-49cc-b410-998ec147902d)
![Figure 15 Highlighted Key Findings in Literature Research](https://github.com/user-attachments/assets/0045f3cb-5d0e-4fc7-8b57-dde1e6d8933d)


