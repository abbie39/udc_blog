# udc_blog
Data exploration of Air BnB data in Boston and Seattle. 

Please find the related blog post here: https://medium.com/@abbie.wright1/boston-vs-seattle-the-great-airbnb-show-down-32687159ed4e

# 1. Installations

Libraries installed:
- pandas = 1.3.0
- numpy = 1.18.5
- matplotlib.pyplot = 3.2.2
- datetime 

Python version = 3.8.3

# 2. Project Motivation

The motivation behind this project was to explore and compare the data for Air BnB listings in Boston and Seattle, with the aims to answer the following three questions:
1. Do Seattle and Boston follow the same pattern of availability? 
2. What is the most popular season for Air BnB rentals?
3. Whereabouts is the highest ranked neighbourhood in Boston?

The reason for choosing each of these questions was as follows:
1. I wanted to investigate if the two cities followed similar patterns of availability over a year, unusual peaks could identify key events that cause a rise in stays. 
2. The most popular season interested me to see if this varied between city, or if certain seasons were popular across the US. 
3. Investigating the highest ranked neighbourhood is useful for considering areas of investment if going into the holiday rental market. 


# 3. File Descriptions
Guide others through the files in your repository. You may not talk about every file here, but you should let them know where they can find the work they might find most interesting.

airbnb_data.ipynb: this is the jupyter notebook where data exploration and plotting was carried out, in order to answer the three questions listed in 'Project Motivation'.

boston_calendar.csv / seattle_calendar.csv: csv file of the availability of listings, imported as a dataframe 'bos_cal' / 'sea_cal'.
boston_listings.csv / seattle_listings.csv: csv file of the listings, with details including review scorings, neighbourhood, and others. 
boston_reviews.csv / seattle_reviews.csv: csv file of the reviews, including reviewer id and comments made.


# 4. Technical details
When your project isn't meant to be interactive or used for other projects, you should instead talk about the technical details of your project. What were your results? What did you do to improve them? What methods did you try? What worked? What didn't work?

First, I took some time to explore the dataframes, taking time to rename columns to avoid confusion between similar column names in different dataframes meaning different things. Additionally I dropped columns that were not going to be relevant for the project, or that contained a large amount of null values.

Then I investigated my first question: do Seattle and Boston follow the same pattern of availability? 
In order to be able to calculate the percentage of properties available, I needed to transform the 'available' column into a true Boolean column. Since data was a critical column in plotting availability I dropped any columns where the date was null. Then I plotted the availability of properties, where data points were given by the percentage available on a given day. 
The results displayed very similar patterns. The major difference was that Boston saw a big dip in availability around April time which is in line with the date of the Marathon which explains the dip in available properties.  


For the second question, 'what is the most popular season for Air BnB rentals?', I first had to convert dates to datetime format in order to extract the month. An issue I discovered at this stage was that running the code for the first question did not plot correctly once date had been converted to datetime. Therefore it is important to run the code in the order it is given. 
I created a function month_season(date) which takes a date in the format of yyyy-mm-dd, and then returns a season depending on the number of the month. This is the schema for assigning the season: 
09, 10, 11 = Autumn
12, 01, 02 = Winter
03, 04, 05 = Spring
06, 07, 08 = Summer
This function was then used to create an additional column in the calendar dataframe using the .apply() function. 

Using matplotlib.pyplot.bar() I plotted a bar chart, which displayed the percentage of properties booked for both Seattle and Boston in a side by side comparison. The results showed Autumn to be the most popular season for Boston whereas Spring was the most popular season for Seattle. 


Finally I approached the third question, 'whereabouts is the highest ranked neighbourhood in Boston?'.
In order to investigate this, I created a new dataframe which was a subset of the original bos_list dataframe, containing the neighbourhood and review related columns. I used the pandas .groupby() function alongside .mean() in order to find the mean values for each column, grouped by the neighbourhood. 
From this stage I then used .iloc to find the neighbourhood correlating to the index of the max score of each review category, which was found using .idxmax(). 

My results showed Brookline to be the highest rated neighbourhood on 5/7 review scoring categories. However I questioned if this data could have been skewed by one or two overwhelmingly positive reviews. 
I looked into how many reviews there were on average in Brookline, and it was just 0.75. Whereas the overall average was 16.04. 
In order to get a fair result I filtered the dataset to only include neighbourhoods who had a mean number of reviews of at least 10 or more.
My findings changed as a result, and the Leather District performed the best as it was the highest rated for 3/7 review scoring categories. 

# 5. Licensing, Authors, Acknowledgements, etc.
Acknowledgements: Completed as part of a Udacity Nanodegree programme, thank you to Udacity for the resources and links to the data.
Data providers: The datasets are part of Airbnb Inside, and the original sources can be found here: http://insideairbnb.com/get-the-data/.

