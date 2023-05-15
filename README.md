# Structured Web Relations Extractor

![](https://img.shields.io/github/license/ulasonat/relevance-feedback-search-engine?color=red&logo=red&style=flat-square)

A powerful information extraction tool that harnesses the Iterative Set Expansion (ISE) algorithm to mine structured data from web sources. This project aims to extract structured relations between entities found on web pages. The program retrieves the top ten Google search results for a given query, extracts the text from each of them, identifies the named entities using spaCy, and applies a pre-trained SpanBERT or GPT-3 model to extract relations between them.
## Contributors <br>
- Ulas Alakent
- Lara Karacasu

## Install dependencies:
```
pip3 install --upgrade google-api-python-client
sudo apt install python3-pip
pip3 install beautifulsoup4
sudo apt-get update
pip3 install -U pip setuptools wheel
pip3 install -U spacy
python3 -m spacy download en_core_web_lg
pip3 install openai
pip3 install requests
```

## Run the program:
```
python3 project2.py [-spanbert | -gpt3] <Google Search API key> <Google Custom Search Engine ID> <OpenAI API Secret Key> <relation> <tuple_count> <query> <top_k>
```
<ul>
    <li><code>-spanbert | -gpt3:</code> Required flag to choose the relation extractor model to use.</li>
    <li><code>&lt;Google Search API key&gt;:</code> Required string argument. This is your Google Search API key.</li>
    <li><code>&lt;Google Custom Search Engine ID&gt;:</code> Required string argument. This is your Google Custom Search Engine ID.</li>
    <li><code>&lt;OpenAI API Secret Key&gt;:</code> Required string argument. This is your OpenAI API Secret Key.</li>
    <li><code>&lt;relation&gt;:</code> Required string argument. This is the relation you want to extract. Valid options are Schools_Attended, Work_For, Live_In, and Top_Member_Employees.</li>
    <li><code>&lt;tuple_count&gt;:</code> Required integer argument. This is the number of tuples you want to extract.</li>
    <li><code>&lt;query&gt;:</code> Required string argument. This is the query to search for.</li>
    <li><code>&lt;top_k&gt;:</code> Optional integer argument. This specifies the number of top results to retrieve from Google Search API. Default is 10.</li>
</ul>

## Files
<b> project2.py: </b> The main program file.
<br> <b> spacy_help_functions.py: </b> A collection of functions to help with spaCy operations.
<br> <b> prompt_1.txt, prompt_2.txt, prompt_3.txt, prompt_4.txt: </b> Files containing GPT-3 prompts for each of the three relations and for selecting new queries.

## Dependencies
The main libraries used in this project are re, ast, sys, requests, spacy, openai, googleapiclient.discovery, and bs4. These libraries are used for regular expressions, representation of literals, command line input handling, web scraping, natural language processing, Google Search API, OpenAI API, and web retrieval respectively.

## Code Structure
The program uses a pre-trained SpanBERT model from the spanbert module for relation extraction. The program defines several functions to perform auxiliary tasks like selecting a new query, truncating text, extracting text from a URL, printing extracted relations, fetching OpenAI completion response, and loading GPT Prompts from external files. In the main function, the program starts by parsing the command-line arguments. Then it initializes variables with the required data, including OpenAI API key, Google Search API configuration, and spaCy language model instance. Afterwards, it annotates the webpage using spaCy and extracts candidate entity pairs. It performs relation extraction on the web pages using either SpanBERT or GPT-3, based on the user's input. Finally, it stores the classified relations, their confidences in a dictionary, and tracks the number of annotations and relations extracted. It outputs k or more tuples satisfying the requested relation.
