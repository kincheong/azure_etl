# Real-time Data Engineering Pipeline for Sentiment Analysis of News Data Using Azure

![image](https://user-images.githubusercontent.com/81759465/222936777-c3e3e450-f523-44d6-ae39-e070b08b571d.png)

This project demonstrates a cost-effective real-time data pipeline for sentiment analysis of news data using Azure services. It demonstrates ETL principles by extracting news data from APIs, transforming it with Azure Functions, and loading it into Azure Cognitive Services for analysis. The pipeline showcases the power of Azure services in creating a cost-effective and efficient solution for sentiment analysis. The pipeline includes the following steps:
 
1. Data Ingestion
2. Data Storage
3. Data Processing
4. Sentiment Analysis
5. Data Visualization ([Link to Dashboard](https://chart-studio.plotly.com/dashboard/kincheong:21/present#/))


## Data Ingestion

To collect news data, I utilized the NewsAPI, a free API that provides up-to-date news articles from various sources. By leveraging this API, I was able to access current and reliable news data without the need to build a web scraper. The NewsAPI can be found at https://newsapi.org/.

![image](https://user-images.githubusercontent.com/81759465/222937062-edca7243-e2d8-441b-a51e-2af45df1ec23.png)

To move the data from NewsAPI to Azure Blob Storage, I used Azure Data Factory, a cloud-based data integration service that enables the creation, scheduling, and management of data pipelines. Azure Data Factory automates the process of ingesting data from NewsAPI into Azure Blob Storage.

One of the drawbacks of using NewsAPI is the limited control over data quality and data sources. Although NewsAPI offers reliable news data, it is impossible to control the quality of the data or the sources it comes from.


## Data Storage

For data storage, I chose to use Azure Blob Storage for several reasons. Firstly, Blob Storage is a cost-effective and scalable option that can handle large amounts of data. Additionally, Azure Blob Storage offers a simple and intuitive interface for managing and accessing stored data.

![image](https://user-images.githubusercontent.com/81759465/222937409-843a6f5e-71c7-4ac3-b816-b7a00dba23a0.png)

While other storage options, such as Azure Data Lake, may offer additional features or capabilities, I found that Blob Storage provided the optimal balance of cost-effectiveness and functionality for my specific use case.


## Data Processing

For real-time data processing, I utilized Azure Functions, a serverless compute platform that allows me to run small pieces of code without having to manage infrastructure. I wrote Python code within Azure Functions to process news data as soon as it was available in Azure Blob Storage. This code is triggered whenever new news data is uploaded to blob storage, which occurs at 14:00pm AEDT daily. The trigger is activated by Azure Data Factory, which calls the latest data from NewsAPI.

![image](https://user-images.githubusercontent.com/81759465/222937886-fb2d1295-7091-4235-847f-d4933c17c5d8.png)

Compared to other Azure solutions, such as Azure Databricks, I found that Azure Functions was a more suitable choice for my use case. While both platforms can handle data processing and analytics, Azure Functions is ideal for my need to run small, event-driven functions quickly and efficiently. Additionally, since Azure Functions is a serverless platform, it is cost-effective and requires no management of infrastructure. In contrast, Azure Databricks is better suited for handling large datasets and complex analytics workloads, but may be overkill for my simple processing needs.


## Sentiment Analysis

For sentiment analysis, I utilized the Azure Cognitive Services API for Text Analytics. To manage costs, I performed sentiment analysis only on the "title" of each news article.

To determine the sentiment of each article, I analyzed the sentiment score of the article's title using the sentiment confidence scores returned by the API. The sentiment confidence score is a value between 0 and 1, representing the level of confidence in the sentiment analysis.

An example of the sentiment analysis result is as follows:
```
AnalyzeSentimentResult(id=0, sentiment=negative, warnings=[], statistics=None, confidence_scores=SentimentConfidenceScores(positive=0.0, neutral=0.39, negative=0.6), sentences=[SentenceSentiment(text=Police treating 19-year-old Krystle Monks's death as suspicious, homicide detectives investigating at Bundamba property - ABC News, sentiment=negative, confidence_scores=SentimentConfidenceScores(positive=0.0, neutral=0.39, negative=0.6), length=130, offset=0, mined_opinions=[])], is_error=False)
```

For an article to have a "Positive" sentiment, the positive confidence score had to be >=0.3. Similarly, for an article to have a "Negative" sentiment, the negative confidence score had to be >=0.3. If the confidence score for both positive and negative sentiments was <0.3, then the article was considered to have a "Neutral" sentiment.

Overall, by analyzing the sentiment of the news articles, we can gain insights into the general tone of the news stories and track trends over time.


## Data Visualization

For data visualization, I opted to use Plotly, a free online tool that offers basic visualization and reporting features. The main reason I chose Plotly over other options, such as PowerBI or Tableau, was that I didn't require a work or school account to access it.

While Plotly can provide helpful visualizations, it has several limitations. First, interactivity with plots is restricted, making it challenging to deliver a comprehensive overview of complex data sets. Additionally, everything in Plotly is code-based, making it less user-friendly than drag-and-drop tools such as PowerBI and Tableau.

Furthermore, Plotly only offers limited types of plots, primarily including tables, text boxes, and graphs. Moreover, the documentation available for Plotly is limited, which can make it difficult to troubleshoot problems or learn new features. Finally, adjusting the position of plots in Plotly can be cumbersome and challenging, with limited options for layout customization.

Overall, while Plotly offers some basic visualization capabilities, it has many limitations, making it challenging to use for more complex data visualization needs.

![Picture3](https://user-images.githubusercontent.com/81759465/222945720-a03dbc69-601d-4761-b00a-e8968c7a31da.png)
<p align="center"><a href="https://chart-studio.plotly.com/dashboard/kincheong:21/present#/">Link to Dashboard</a></p>


# Conclusion
Using these Azure services allowed me to build a cost-effective real-time data pipeline for sentiment analysis of news data. However, the specific tools used will depend on the complexity of the project, the size of the data, and the specific requirements. 
