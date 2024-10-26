# ECE 522 Project 1

## 0. Group Members: 
| Name      | ID      |
| ------------- | ------------- |
| Yicheng Yang | 1647241 |
| Jiale Cai | 1815497 |
| Zhouyiyang Yang | 1868452 |
| Yulong Zhang | 1823084 |
___

## 1. Dependencies
#### 1.1. Core dependencies
- **yahoo_finance_api**: This is the core library of the project. This library allows you to call the Yahoo Finance API and quickly query and obtain necessary data. Additionally, compared to other Yahoo Finance libraries, this library offers the latest API and has been maintained by contributors up until recently, which is why this library was chosen.
- **plotters**: The plotters crate is a drawing library designed for data plotting. It supports rendering figures, plots, and charts in various formats, including bitmap, vector graphics, and WebAssembly3. This crate is perfect for visualizing data in project, whether we are creating simple charts or complex visualizations.
#### 1.2. Side dependencies
- **clap**: This is a library for parsing command-line arguments. It not only allows for easy retrieval of parameters but also provides a quick way to generate help documentation for the --help command.
- **tokio-test**: This is a library of testing utilities supported by **tokio**. The main purpose of importing this library is to support the operation of **yahoo_finance_api**.
- **time**: The time crate provides functionality for working with dates and times. It offers a variety of features such as formatting, parsing, and manipulating dates and times with nanosecond precision1. This crate is useful if we need precise control over time calculations and formatting in project.
- **chrono**: The chrono crate is another date and time library for Rust, but it focuses on providing timezone-aware and timezone-naive date and time types2. It supports parsing and formatting with a strftime-like syntax and can handle various time zones. This crate is ideal if the project requires handling different time zones or performing complex date and time manipulations.
---
## 2. Financial analysis algorithm
#### 2.1. Data Retrieval and Validation
- **get_by_symbol**: This function retrieves historical stock quotes for a given symbol using the Yahoo Finance API. It handles invalid input and missing symbols, ensuring only valid data is processed.
#### 2.2. Data Transformation
- **vec_quotes_to_closing_prices**: Converts a vector of **Quote** objects into a vector of tuples containing the date and closing price. This transformation simplifies further analysis.
#### 2.3. Volatility Detection
- **find_volatile_days**: Identifies days with significant price changes (greater than 2% variation) by comparing closing prices of consecutive days. This helps in detecting volatile trading days.
#### 2.4. Min/Max Price Identification
- **find_min_max_closing_prices**: Finds the minimum and maximum closing prices within the given data, along with their corresponding dates. This is useful for understanding the price range over the period.
#### 2.5. Data Visualization
- **print_closing_prices_and_dates**:  Prepares data for plotting and calls the **plot** function to generate a visual representation of the closing prices, highlighting volatile days and annotating min/max prices.
#### 2.6. Plotting
- **plot**:  Uses the **plotters** crate to create a chart of the stock’s closing prices over time, marking volatile days and annotating the minimum and maximum prices.
---
## 3. Chart Setup
#### 3.1. Chart Type
- **Scatter Plot**: The project uses a scatter plot to display closing prices over time. Each point represents the closing price on a specific date.
#### 3.2. Autoscaling
- **Autoscaling**: The code calculates the minimum and maximum closing prices to set the y-axis range dynamically. This ensures that the chart scales appropriately to fit the data, making it easier to visualize trends and significant price changes.
#### 3.3. Axis Features
- **X-Axis**: The x-axis represents the dates. The code uses a formatter to display dates in a readable format. It also sets the number of labels to ensure the axis is not cluttered.
- **Y-Axis**: The y-axis represents the closing prices. The range is set based on the minimum and maximum prices found in the data, ensuring that all data points are visible within the chart.
#### 3.4. Axis Features
- **Volatile Days**: The code marks volatile days with blue circles and vertical lines, making it easy to identify days with significant price changes.
- **Min/Max Prices**: The minimum and maximum prices are annotated on the chart with text labels, highlighting these key points.
#### 3.5. Error Bars
- **Error Bars**: The code includes error bars for volatile days, showing the high and low prices for those days. This provides additional context about the price range on volatile days.
---
## 4. Project Setup
1. To run this project, you first need to ensure that **Rust** is installed on your computer. You can visit the following website and follow the tutorial to install **Rust**:
	- https://www.rust-lang.org/learn/get-started
2. Secondly, please clone the project code from the following URL using Git or download it directly as a ZIP file:
	- https://github.com/Yulong0425/ECE_522_Proj1
3. Navigate(**cd**) to the working directory via the command line and enter: ***cargo update***, to fetch the required dependencies.
---
## 5. Usage Instructions
Navigate(**cd**) to the working directory via the command line and enter: ```cargo run -- -n (stock symbol)```, to run the project. **(stock symbol)** represents the name of the stock you want to query. For example, the following command will retrieve stock ticker data of *Apple Inc.*:```cargo run -- -n AAPL```
You will see data regarding **volatile days** and **minimum/maximum prices**, and an image named **"plot.png"** will be generated in the root directory of the project.

Additionally, after building with: ```cargo build (optional '-r')```, you can find the compiled program in the ```./target``` folder. You can also run the program directly using the following command: ```./target/debug(or release)/project -n AAPL```

For a more detailed description, please run with ```--help``` as an argument