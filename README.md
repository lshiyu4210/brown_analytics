## Spark Project

The data you need for it can be found in files/data/SparkProject. The due date for this project is Friday Dec 6th. 

You work for a data analytics company called Brown Analytics, which has secured a new project to analyze advertising data. Your client is an ad exchange platform, Ads Are Us, which serves a number of advertising clients. You are the lead on this project. Ads Are Us places ads for a variety of consumer products on a number of online publishing platforms. They would like to have insights into the likelihood of an ad for a certain type of product being clicked on given the sentiment of the surrounding textual content and the gender and age group of the viewer. For example, a question they may want to answer is: what is the likelihood of an ad for a electronics product to be clicked on if the surrounding textual content is positive and the gender of the user is female.

Based on the data provided to you, you need to come up with a set of recommendations regarding ads for which products should be placed in which kind of textual content taking into account the sentiment of the textual content, the gender and age group of the viewer of the ad. You are NOT required to build a predictive model or a recommendation system. The goal for the project is to ingest the data and perform relevant analysis based on which you will make recommendations for the client.

Data:
You are provided with three csv files described below. The files can be downloaded from files in /Data/SparkProject.

1. A log file in csv format which consists of rows that contain the following type of information:
- sentiment, publication_URL, product_URL, got_click, gender, age_group (an actual log file might contain more information such as a timestamp, ip address, etc. but for simplicity this log file is ). For example, a row may contain the following information: {Positive, https://nytimes.com, https://vitamix.com/blenders, 1, female, middle-age}
- sentiment records the sentiment of the textual context in which an ad was displayed to a viewer. It is NOT the sentiment of the ad. Sentiment has 3 values: Positive, Neutral, Negative.
- publication_URL is the URL of the (online) publication in which an ad for a specific product (e.g., Vitamix blender) appeared. For simplicity, let us assume that even if the product has several models (versions) the ad is model-agnostic.
- product_URL is the URL of the brand’s page for that product on its eCommerce site. (e.g. https://Vitamix.com/blenders). It is intended to be the same URL as the product_URL in the csv ‘products’.
- got_click is a binary variable that records whether the viewer to whom the ad was displayed clicked on the ad or not. You may assume it is 0 or 1, where 1 records that it was clicked on.
- gender is the gender of the person to whom the ad was displayed. Possible values for gender are male, female, non-binary.
- age_group records the age_group of the person viewing the ad. The values are among ‘juvenile’, ‘young’, ‘middle-age’, ‘senior’.
2. The products.csv consists of (comma separated) rows which contain product (name), product_URL, and product_type
- product (name) records the product name, which includes the brand (e.g., Vitamix blender).
- product_URL records the page of the product on the brand’s page for that product on its eCommerce site. (e.g., https://Vitamix.com/blenders). For simplicity, all the different models of blender by Vitamix share this page. (This is the gold standard in terms of which Product_URL entries in the log file are validated as correct or corrupted in case there are any that are malformed. We have tried to make sure they are all correct, but please let us know if you find any that are not correct.)
- product_type contains the type of the product (e.g. blender, in our running example)
3. product_categories contains information about the broad category a product may belong in. Attributes of product_categories:
- product_type: for example, blender or lipstick or computer (does not include the brand or model number). Same as ‘product_type’ in ‘products’ table
- category: the generic category of the product (e.g., small kitchen appliances or cosmetics or electronics)

You are required to do the following tasks using PySpark (not Python or R). You may do it on DataBricks platform or install PySpark on your computer and do the analysis using PySpark on your computer. Please make sure to show all the work by which you get results in the following questions.

- For each product, compute all the Publication_URLs containing an ad for that product.
- For each product type, compute all the Publication_URLs containing an ad for that product type.
- For each product, compute the click rate for it. Click rate is the number of times a display of an ad was clicked on (by any user) divided by the number of times it was displayed (to any user). Note the click rate is not specific to each user.
    - For each product, compute the click rate for each sentiment type
- For each product type, compute the click rate for it.
    - For each product type, compute the click rate for each sentiment type
- For each category, compute the click rate for it.
    - Similar to above, for each category compute the click rate for each sentiment type
- Choose a product randomly; determine if there are any 'significant' differences in the click rate between positive and negative sentiment type of the ad context for that product type given the gender of the viewer.
    - You can use any form of statistical testing to calculate "significance" that you like. Eg. you assume a binomial distribution for click rate and use a z-test. Compute these figures for all 3 genders.
- For extra credit, explore the data in whatever way you feel would be valuable to make recommendations to the client. This type of analysis in the real world would be very open ended and you could take it in whatever direction that interests you.