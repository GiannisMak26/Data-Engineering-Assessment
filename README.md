
# Credit Lending Product

The goal of this project is to inject data from various sources and assess the quality of the data. It curates the data based on business rules in one standard file format, following a fixed template. 

This is part of the ABN AMRO's Assessment for the Junior Data Engineering position.

## Description

### Files

This project consists of specific files to address the pipeline requirements. To begin with, three files have been created:

1. **stocks.json**: Generated using the Yahoo API, this file contains weekly stock values. The generated stock prices are collected in real-time, with the most recent closing date being from yesterday. Each entry in this JSON file consists of three values: "symbol" and "date" (string type) along with "closing_value" (float type).

2. **clients.csv**: This file includes information about the clients, such as their "id", "profile", "address", "corporate_information" (for companies), "email", "telephone", "client_since", "nationality", "has_loan" (indicating if they already have a loan), and "Next_payment_date".

3. **collaterals.csv**: Contains information regarding the assets owned by the clients. It includes "id" of the client, "type" of the asset, "asset_name", and "value_current" (correlating to its stock value).

## Implementation

### Prerequisites

The Python 3.10 code was run locally on the Google Colab environment. The 'clients.csv' and 'collaterals.csv' files must be first uploaded to the Google Colab server every time a new runtime session is initiated.

Packages required to run the code:
- **yahoo_fin**: Allowing the user to download historical stock price data, along with real-time information
- **pandas** and **JSON**: Used to read the newly created dataframes.
- **datetime**: Used to obtain the required dates.

### Code Execution

The implementation of the code can be divided into two main components:

1. **Fetching Stock Data**: The  Python script fetches stock data for a list of specified stock symbols, taken from Yahoo Finance in the past week. It will then extract the start and end dates of that period, along with the corresponding closing values of each stock at the beginning and end of the week. Finally, it will store this information in a JSON file called "stocks.json".

2. **Processing Financial Data**: This component reads 'collaterals.csv' and 'clients.csv' into Pandas DataFrames. It initializes a new column 'value_past' in 'collaterals.csv' and loads JSON data from 'stocks.json'. Functions are defined to obtain closing values from stock assets over the current day and 7 days ago. The algorithm iterates over rows in 'collaterals.csv', updating columns based on asset types and calculating fluctuations in stock values. Finally, it merges relevant columns from 'collaterals.csv' with 'clients.csv' based on their common 'id' column, prints the resulting merged DataFrame, and exports it to 'merged_data.csv'.

