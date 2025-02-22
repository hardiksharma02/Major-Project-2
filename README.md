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

## Installation
This project requires Python 3.9 or higher. Follow these steps to set up the environment:

1. **Set up a virtual environment**:
   ```bash
   $ python3 -m venv .venv
   $ source .venv/bin/activate
   $ pip3 install -r requirements.txt

   
