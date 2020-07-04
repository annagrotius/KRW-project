Hypothesis Generation Project
=============================
A knowledge graph tool that can aid a researcher in generating new hypothesis ideas from data related to coronavirus research.

## Introduction
This project is by Marta Turek, Anna de Groot, and Marcin Michorzewski and is for the course Knowledge Representation on the Web at the Vrije Universiteit Amsterdam, taught by Ilaria Tiddi and Albert Moreno. The work in this project develops a hypothesis ontology that is used to build a knowledge graph with sources on the web. A Web API application is built around a use case that demonstrates the ontology model. Our research question investigates how the knowledge graph can aid a researcher towards generating new hypothesis ideas. 

## Content
* The directory **'sparql-queries'** contains the file queries.rq where links to each query is stored. The results of these queries are also in this directory. 
* The content to build the Ontology can be found in the directory **'Ontology'**.
* The notebooks for building the graphs can be found in the directory **'Parsing'**. In this directory, the directory **'outputs'** contains the created subgraphs.
* The directory **'mesh'** contains the notebooks and files to create the graph containing all mesh related triples. 
* The **'Extracting-keyowrds'** directory contains the materials needed to preprocess the hypotheses for their keywords.
* The **'Linking'** directory contains the notebooks and output graphs for linking the keywords, named entities, and MeSH concepts.

## Running the Code
All code is written in Python 3.7 notebooks and should be compiled in the order described hereunder. The library requirements are RDFlib, Owlready2, and SpaCy.

NOTE: filepaths are written according to how they are saved when running the notebooks in order. 

#### Step 0:
Ensure that all queries from sparql-queries/queries.rq were executed and that the respective output results are in the directory sparql-queries. The following files sould be there: abstract-info-instances.csv, bnode-instances.csv, hypothesis-info-instances.ttl, paper-info-instances.ttl, and provenance-info-instances.ttl.

#### Step 1:
Preprocess abstract data using the notebook Extracting-keywords/generate_hypothesis_entities.ipynb. The output of this notebook is called paper_hyp_entity_data.csv.

#### Step 2: 
Create first subgraphs. After running the notebooks, the output graph can be found in Parsing/outputs/.
- Run notebook Parsing/main-graph-parser.ipynb. This script requires the files hypothesis-info-instances.ttl, paper-info-instances.ttl, and provenance-info-instances.ttl. 
- Run notebook Parsing/bnode_csv_parser.ipynb. This script requires the file bnode-instances.csv.
- Run notebook Parsing/keyword_instances_parser.ipynb. This script requires the file Extracting-keywords/paper_hyp_entity_data.csv.

#### Step 3:
Run notebook mesh/mesh.ipynb to obtain the graph of the mesh triples.

#### Step 4:
- Link keywords (/Parsing/outputs/hypothesis-keywords-graph.ttl) and named entities (Parsing/outputs/bnode_graph.ttl) using notebook Linking/linking_instances.ipynb
- Link keywords ((/Parsing/outputs/hypothesis-keywords-graph.ttl) and mesh instances (mesh/mesh_graph.ttl) using Linking/linking-mesh.ipynb.

#### Step 5:
Merge all graphs into the complete knowledge graph using Parsing/create_final_graph.ipynb. The complete knowledge graph is the turtle file Parsing/outputs/complete_graph.ttl.





