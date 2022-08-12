# Creating Synthetic Data

Because of privacy reasons related to the geographical datasets, we had to create synthetic datasets to run our manipulation and visualization demos for this repository. Below is a description of what we did to create the synthetic data. To see the code for how we did it, view the `synthetic_data_creation.ipynb` file in this repository.

## Datasets we Worked With
- Location Dataset: Included information about the location of the Reddit users with columns such as "Country", "State", and "City".
- Time/Long/Lat Dataset: Included information about the exact location of Reddit posts, their timezone, and the time in which they posted on Reddit in Unix format (number of seconds since January 1st, 1970 at 00.00.00 UTC).
- Subreddit Dataset: Includes more information about subreddit posts with columns including author, id , subreddit and time of post.
- Demographic Dataset: This dataset includes information about subreddits by providing variables such as age, gender, partisanship, and affluence, all measured as percentiles which are relative to each other. It also groups subreddits into categories such as "Self-Improvement", "Politics", and "Gaming".

## Location and Time/Long/Lat Dataset

### Preparing Data for Conversion

Before we started working on converting the usernames in the location dataset, we needed to prepare our data with proper column names and make sure that we were only working with data within the US because that was what we needed for our choropleth visualizations.

### Creating and Adjusting Fake Usernames
Once the data was adjusted, we went ahead and created the fake usernames. To do this, we ran a for loop iterating through every row in the dataset and added a new column titled 'author_synthetic' where every row contained 'user_x' where x is the index number for that author.

Once the 'author_synthetic' column was created, we moved it to the front to organize our dataset and make it easier to compare with the author column. We then made sure we dropped all `NaN` values in the dataframe.

### Taking Random Sample

Next, we took a random sample of 100 rows of the dataframe using the `.sample(n=100)` function. This way, we ensured that the authors we were using were completely random. However, we won't drop the 'author' column yet because we used it to merge the data frame on the next step.

We then loaded the dataframe with author, latitide, longitude, and time information. Since the location data we just manipulated and this data frame shared the 'author' column, we merged them using the `.merge()` method. By merging with the "author" column, we ended up with a dataframe that included the information of both datasets. This meant that the fake usernames we created for the authors in the previous data frame, were paired with the authors in this data frame as well. After doing this, we dropped the `NaN` values once again.

### Creating Final Data Frames with Fake Usernames

Finally, we extracted the columns of this data frame that were included on the original datasets, but we replaced the 'author' column with the 'author_synthetic' column. This way, we ensured that the data in both data frames was going to be paired with the correct fake username, but we didn't show the username of whoever revealed their information.

## Subreddit Dataset

### Preparing Data for Conversion

For this third dataset, we read it in as a `.csv` file and made sure that we dropped the duplicate authors so that we worked with a variety of users. Next, we switched the columns so that they were all titled with a name that related to the information they contained. Finally, we dropped an "index" column which was irrelevant for our visualizations so that this data frame could load faster in future steps.

We then continued to drop unnecesary columns so that we could merge it with the previous data frame that included all the data from the combined datasets.

### Merging Data Frames

We then merged this dataframe with the combined dataframe we created previously using the 'author' column. This ensured us that the fake username would once again be paired to the correct 'author' information they are covering.

### Creating Final Data Frames with Fake Usernames

Finally, we once again selected only the columns that were useful for our visualizations and that were included in the original dataset. However, we replaced the 'author' column with the 'author_synthetic' column to protect the users' privacy.

Since one of our first data wrangling demos shows how we originally merged all these files, we separated the data frame into 4 datasets of 25 rows so that this synthetic data can be used in testing the first merging demo.

## Saving the Data Frames as Parquet Files
To finish this process, we used the `.to_parquet()` method to save these data frames as `.parquet` files. This allows for faster loading time when we load the files into the demos we prepared.