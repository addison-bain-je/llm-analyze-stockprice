# Using GPT-4o for Data Analysis
Using Azure AI Assistants (Code Intepreter) for Data Science
<br> Let's see if we can automate data analysis on the Nvidia stock price data.
<br> I will be using the <b>gpt-4-32k</b> model deployed in my Azure AI Hub.
<br>
<br>
For this example, I am going to use the NVIDIA stock price dataset.
<br>You can download it ![here](nvda_stock_data.csv) and upload the CSV file into the Assistants playground.
<br>
<br> Below is the system instruction (prompt) that I set up in the Assistants playground.
<br> `You are an expert Business Intelligence Analyst who will be fielding questions about stock price of Nvidia.`
<br>
## Exploratory Analysis
As a data analyst, typically we want to have a quick overview of the dataset we are dealing with.
<br>So let’s explore this dataset first. You can try the following prompts:
* Describe the fields in the dataset.
* Show head and tail of this dataset.
* What is the shape of this data?
* Give me statistical information of the columns.

![Describe fields](images/Image1.png)
<br>
![Shape of data](images/Image2.png)
<br>
![Shape of data](images/Image3.png)
<br>
![Statistics](images/Image4.png)
<br>
<br> Observe how the LLM has converted your prompts from natural language to python code, and execute the python code to generate the results, and then provide summarized response back in natural language.
<br>
<br> From the responses above, we get a sense of the dataset on hand, for example, the stock price and trading volumne from 02/Jan/2020 to 03/May/2024, as well as basic statistics across this period.
<br>
## Data Visualization
A picture (or visual) speaks a thousand words. Let's see how we can automate data visualization tasks.
### Monthly Returns
Assuming you buy Nvidia's stock at the start of the month and sell it at the end of the month, how much you will earn?
<br>Let’s use this prompt to generate a bar plot to visualize this.
<br>
`Provide this: Bar Plot of Monthly Returns in percentage over time, 
Date column should include this Month- Year instead of dates day by day.`
![Box-plot 1](images/Image5.png)
<br> We can oberve that there is a positive stock returns on most months. If you had held this stock over the entire period, you would have likely accumulated a decent gain :)
<br>
### Line Plot With Trending Events
<br> Now, we want to know how the stock price has changed over time and see if we can correlate key events to these changes.
<br>
`Create a plot of adjusted close price over time with annotations for significant events. 
The dataset contains the 'Date' and 'Adj Close' columns. 
Identify significant events based on major changes in the stock price and annotate them on the plot.`
<br> Here's the initial line plot, which looks super messy. The model seems to have made an incorrect assumption, and basically marked all changes as significant.
![Line-plot 1](images/Image6.png)
<br> Let's correct its assumption and only consider those changes which are more 3 standard deviations.
<br> We can use this prompt:
<br>
`Please revise the line plot. Only those changes which are more than 3 standard deviations should be considered significant.`
![Line-plot 2](images/Image7.png)
<br>
<br>
### Get Multiple Charts
If you have absolutely no idea what to analyze, perhaps you can try your luck to see what the model can keep up with automatically:
<br>
`Show me 3 different graphs that can provide different information and meaningful insights.`
![multiple-plot 1](images/Image8-1.png)
![multiple-plot 2](images/Image8-2.png) ![multiple-plot 3](images/Image8-3.png) ![multiple-plot 4](images/Image8-4.png)
<br>
<br> 
## Additional Notes
### Python Execution Error
Sometimes you may observe that the AI Assistant encounters some error when excuting the Python script, perhaps due to issue with environment or even syntax error.
<br> Generally, the AI Assistant should be able to self-correct and re-run the script, as shown below:
![Error](images/Image9.png)
<br>
### Correlate with actual world events
Remember the plot above where I marked out the signficant changes in stock prices?
<br> What if we can correlate those data points with actual world events that happened in the past?
<br> Currently, Azure AI Assistant does not have access to the Internet or web resources.
<br> A further improvement could be to incorporate a Function that calls a Web Search API, so that the LLM can also refer to news articles from the Internet and supplement its analysis and responses.
