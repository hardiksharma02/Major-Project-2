# Patent Classification Project

## Overview
The goal of this project is to train a machine learning classifier that can automatically classify international patents downloaded from the WIPO website into one of eight categories based on the textual content of their titles and abstracts.

## Data Source
- Patent data is available as raw XML from the [USPTO Bulk Data Storage System](https://bulkdata.uspto.gov/).
- Each large zipped file contains a single file with multiple XML blocks.

## Classification Categories
The patent top-level section labels of interest are as follows:
- **A**: Human necessities
- **B**: Performing operations; transporting
- **C**: Chemistry; metallurgy
- **D**: Textiles; paper
- **E**: Fixed constructions
- **F**: Mechanical engineering; lighting; heating; weapons; blasting
- **G**: Physics
- **H**: Electricity

**1.Installation**
This step assumes that **Python 3.9+** is installed. Set up a virtual environment and install from requirements.txt:

    $ python3 -m venv .venv
    $ source .venv/bin/activate
    $ pip3 install -r requirements.txt

For further development, simply activate the existing virtual environment.

    $ source .venv/bin/activate

Download and install **spaCy** language model
Within the activated virtual environment, once the dependencies are installed from requirements.txt, run the following command:

    $ python3 -m spacy download en_core_web_sm

This provides the standard (small) spaCy's English language model for downstream lemmatization, explained below.

Download and place a file of stopwords
For stopword removal (to train a linear model), we need a stopwords file. The NLTK English stopword list is downloaded to the file stopwords.txt, placed at the root level of this repo.

**2.Preprocessing**
The preprocessing script requires that an unzipped raw XML file (with information on hundreds of patents) exists in the raw_data/ directory. As an example, the following file is downloaded from the source, uncompressed, and stored in the below path in XML format:

    raw_data/ipgb20200107_wk01/ipgb20200107.xml

Because the large XML file is not directly parsable, it needs to be broken down into individual blocks, each of which constitute a valid XML tree. This can then be parsed, and the relevant information extracted. Using this approach, we can organize the information into a form that can be used to train an ML classifier.

Run the preprocessing script (after editing the path to the raw data appropriately) as follows:

    $ python3 preproc.py

This produces a new directory with clean, parsable XML files, and writes out the data to a JSON file (data.json). The JSON data consists of the following key-value pairs:

    data = {
        "doc_id": doc_id,
        "title": title,
        "abstract": abstract,
        "label": section_label,
    }

Note that the **section_label** field here refers to the top-level of the classification hierarchy (8 categories, from A-H).
