# DS 3500 Final Project: NLP and ML Methods to Predict Stock Price Change from Earnings Call Transcripts

## Contributors: 
Xinyu Wu, Marco Tortolani, Qi Li, Emily Wang, Kelly Phalen

## Intro:
Welcome to our investigation towards predicting the stock market with the use of natural language processing and machine learning! This project is the result of a semester of collaborating after classes, and we’re happy to show you how we put all these moving parts together, from labeling -> cleaning -> storing-> tuning-> testing

## Overview:
The goal of the project was whether we can create an ML model that can use an earnings transcript (or similar financial document) to make a prediction on whether a stock’s price will move up or down. For example, given that an earnings call for Apple (NYSE: AAPL) released on the morning of 12-23-2018, can we predict a positive or negative movement in price at the close of 12-24-2018. 

## Requirements:
Software:
- MongoDB Community Server
- Python 3
Libraries: 
- $ pip install -r requirements.txt

## Running:
Although we have yet to implement a main class to limit the function calls, we have used the jupyter notebook files (such as ‘ds3500_presentation.ipynb’ or ‘starbucks_demo.ipynb’) as examples to how to structure code. Most of the variables such as transcript file locations can be isolated to the beginning of the project. Variables that dont directly reference file locations or ticker names can go generally untouched. The output of the pipeline, if successful, should be the average performance of the stock by machine learning model (by accuracy)


## File structure:
This project code involves 6 classes in total, each with their independent file:
- Transcripts.py
- PerformanceTester.py
- StockPuller.py
- PDFCleaner.py
- Database.py

For this project, the jupyter file, models_visualizations_demo.ipynb provide an example of how to set up the pipeline to either analyze many stocks or a chosen subset of stocks. Lastly, the transcript folder (named ‘transcripts’) should consist of raw earnings call transcripts used for training the model (40 largest NASDAQ and S&P 500 companies by market cap), organized as such: 
- Transcripts
  - AAPL_transcripts
    - 20180501_Apple_Inc-_Earnings_Call_2018-5-1_FS000000002423660030.pdf
    - 20180201_Apple_Inc-_Earnings_Call_2018-2-1_FS000000002396280466.pdf
    - 20180913_Adobe_Inc-_Earnings_Call_2018-9-13_FS000000002467037691.pdf
  - ADBE_transcripts
    - 20170620_Adobe_Inc-_Earnings_Call_2017-6-20_FS000000002358292240.pdf
    - Etc.
  - Etc.

Note that for the transcript files, the stock ticker is apparent in the subfolder, and the date is apparent in the file name. This is essential for the project to label files correctly. Pulling files from a bloomberg terminal will automatically name your files appropriately; otherwise, manual date tagging may be necessary.

## Class Descriptions:
- PDFCleaner.py
    - Takes a pdf file of an earnings call transcripts, scrapes it for text, and returns the cleaned version of the text. This will be essential for preparing large amounts of text data for processing.
- StockPuller.py
    - Pulls stock data from yahoo finance for requested ticker, and depending on timeframe selected (preset to 1 day), will return whether a stock’s price moved up or down (1 or 0) after that timeframe.
- PerformanceTester.py
    - Runs StockPuller on a list of stocks baased on the provided tickers and dates. Creates a list of ints or floats that can be used as a classification label when appended to the rest of the transcript data.
- Store_transcripts.py
    - Initializes MongoDB database and stores transcripts, ticker names, dates, and stock performance labels into database. Will be crucial for model training and testing, as cleaning and moving the transcripts takes a long time.
- Transcripts.py
    - Reads all transcripts from folder, uses PDFCleaner.py to clean all transcripts, and creates a dictionary with transcripts and matching stock price change data.
- Database.py
    - Establishes connection with MongoClient and creates transcript database with transcripts from each ticker.

## Acknowledgement:
We thank Professor John Rachlin for providing us the preparation and the space to develop this project fully. We would also like to thank TA’s Samar Dikshit and Oleks Litus for their guidance in how to best approach the problems involved with text cleaning and nlp.
