# Medical Abbreviation Disambiguation

## Table of Contents
- [Description](#description)
- [Installation](#installation)
- [License](#license)
- [Acknowledgments](#acknowledgments)
- [Roadmap](#roadmap)
- [Support](#support)
- [Further information](#further-information)
- [Dependencies](#dependencies)

## Description
This project demonstrates methodologies for tackling Abbreviation Disambiguation (AD) in the medical field using Natural Language Processing (NLP) techniques. The primary goal of AD is to associate abbreviations in sentences with their corresponding full forms from a set of potential expansions.

## Installation
- **Dataset**: The dataset used in this project is available on Kaggle [here](https://www.kaggle.com/datasets/xhlulu/medal-emnlp). You can either run the notebook using Google Colab and place the dataset in the respective directories as mentioned in the initial cells, or modify the file paths to specify your preferred dataset location.
- **GPU (optional)**: While not mandatory, a GPU is preferable for improved performance.
- **Dependencies**: All necessary dependencies will be installed when you run all the cells in the notebook.

## License
This project is released under MIT.

## Acknowledgments
We would like to express our gratitude to the following individuals who have contributed to this project:
- Fatemeh Ranjbaran
- Parvaneh Soleimany

## Roadmap
In future developments, we plan to employ more robust models such as BIOGPT, which is three times larger than SCIBERT, with a .bin file size exceeding 1.5 GB.

## Support
For any support or inquiries, please contact us at [email](mailto:mohammadrez.hossein2@studio.unibo.it).

## Further information
You can find much more detail in the PDF report file along graphs and visualizations.

## Dependencies
The project mainly relies on the following dependencies:
- torch
- transformers
- datasets
- matplotlib
- nltk
