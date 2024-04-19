# **mars_news_weather_scraper** #

--------

## **Project Goal** ##
* This project leverages web scraping techniques to extract and analyze data from NASA's Mars Exploration Program website "https://static.bc-edx.com/data/web/mars_news/index.html" and "https://static.bc-edx.com/data/web/mars_facts/temperature.html". This project reinforces core data science skills like data collection, organization, analysis, and visualization. The project consists of two parts:


**Part 1:** Mars News Article Scraper: Develop a script to scrape titles and preview text from Mars news articles on the website. This exercise strengthens the ability to identify and extract specific HTML elements using Beautiful Soup.

**Part 2:** Mars Weather Data Scraper and Analyzer: Create a script to scrape weather data presented in a table format on the website. This part involves parsing HTML tables and performing data analysis tasks to summarize and visualize the weather data.

--------

## **Scraped Data Outputs:** ## 
* The data from both "part_1_mars_news.ipynb" and "part_2_mars_weather.ipynb" are saved as .json and .csv respectively in the folder called "scrapping_output_data"

**Part 1 - .json**

![Screenshot 2024-04-18 115202](https://github.com/nmrodio/mars_news_weather_scraper/assets/157527614/f566a7bc-eceb-493e-a20f-8683c0cdb3d3)


**Part 2 - .csv (Only showing the first 25 rows in screenshot)**

![Screenshot 2024-04-18 115231](https://github.com/nmrodio/mars_news_weather_scraper/assets/157527614/34355f3e-abe6-4083-bf50-db630e1eaca9)

-------

## **part_2_mars_weather.ipynb Graph Results:** ## 

![Screenshot 2024-04-18 115824](https://github.com/nmrodio/mars_news_weather_scraper/assets/157527614/ddcb06e8-de44-4b2e-8a81-1f919f694509)

![Screenshot 2024-04-18 115835](https://github.com/nmrodio/mars_news_weather_scraper/assets/157527614/1e9d45e9-b404-453b-9633-b9bf7a949daf)

![Screenshot 2024-04-18 115906](https://github.com/nmrodio/mars_news_weather_scraper/assets/157527614/56b5339e-0400-4e19-82a3-081d6ff4d95e)

![Screenshot 2024-04-19 142936](https://github.com/nmrodio/mars_news_weather_scraper/assets/157527614/e9b4c55a-3637-441f-bab8-1f3f0ab63c2e)



-------

## **part_2_mars_weather.ipynb Weather Analysis:** ## 

#### **Which month, on average, has the lowest temperature? The highest?** ####

On average, the coldest month on Mars in the third month with the forth month being almost just as cold but the third month is slightly colder on average. The eighth month is the warmest with the ninth month being a very close second warmest. As show by the graph above titled "Average Temperature by Month (Coldest-to-Hottest)", Mars tends to have colder months in the first half of its yearly cycle with the warmer weather coming towards the back half of the year. Although the last half of months on Mars tend to be warm on average these tempetures of far below freezing (0 degrees Celsius / 32 degrees Fahrenheit) year round is extremely cold in human terms compared to the weather that we experience here on Earth. 

#### **Which month, on average, has the lowest atmospheric pressure? The highest?** ####

On average, the atmospheric pressure is lowest on Mars in the sixth month. The atmospheric pressure is highest on Mars in the ninth month. There seems to be no pattern between when the atmospheric pressure increases or decreases but as shown by the graph above titled "Average Atmospheric Pressure by Month", it seems like the atmospheric pressure tends to be lower on Mars during the "middle" months of the year (4,5,6,7).

#### **How many terrestrial days exist in a Martian year?** ####

As shown by the graph above titled "Minimum Temperature in Earth Days over Martain Years" The distance from peak to peak is roughly (875-200), (1550-875), or 675 days. A year on Mars appears to be about 675 earth days from the plot. Internet search confirms that a Mars year is equivalent to 687 earth days. 

-------


## **How does the code work?** ## 
### **part_1_mars_news.ipynb** ###
1) Importing necessary dependencies (MOST IMPORTANT: "from splinter import Browser" and "from bs4 import BeautifulSoup as soup")
2) Chrome browser is defined
3) The website URL (https://static.bc-edx.com/data/web/mars_news/index.html)  that will be used for the web scraping is defined and stored as a variable called "url"
4) "browser.visit(url)" is then used tell the code to visit that URL
5) "browser.html" is then used to pulling the the website content as HTML and is stored as a variable called "html"
6) Then the Beautiful Soup html parser is created using the library imported above and the parser is stored in a variable called "soup"
7) Then all the text elements are extracted
8) Next an empty list is created called "mars_data_list" to store the data that will be extracted from the website that we want => A for loop is used to extract the article "titles" and "previews" based on the html elements found from inspecting the website ==> These results are stored into a dictionary called "mars_data_dict" and then that dictionary is appended into the empty list "mars_data_list" ===> The list is then printed to confirm that the "titles" and "previews" were extracted correctly and are infact a list of dictionaries
9) The "mars_data_list" results are then turned into a pandas dataframe and the results stored into a folder called "scrapping_output_data" and a file called "mars_news" as a .json
10) Lasty, "browser.quit()" is used to close the website

### **part_2_mars_weather.ipynb** ###
1) Importing necessary dependencies (MOST IMPORTANT: "from splinter import Browser" and "from bs4 import BeautifulSoup as soup")
2) Chrome browser is defined
3) The website URL (https://static.bc-edx.com/data/web/mars_facts/temperature.html)  that will be used for the web scraping is defined and stored as a variable called "url"
4) "browser.visit(url)" is then used tell the code to visit that URL
5) "browser.html" is then used to pulling the the website content as HTML and is stored as a variable called "html"
6) Then the Beautiful Soup html parser is created using the library imported above and the parser is stored in a variable called "bs"
7) Then all the "rows of data" are extracted to see what we are working with to eventually grab the data from the table on the website
8) An empty list called "data_list" is created to store the rows of data from the table => All the whole table is found using the overall "tr" html element that holds the data from the table ==> Then a for loop is used to find the actual data points we want from the graph which are in the HTML element "td"===> A new empty list is created called "row_l" to store the data that is extracted into a list for each "row of data" and another for loop is created and nested inside the first for loop ====> The extracted data is then cleaned of HTML elements using ".text.strip()" and then appended into the "row_l" list =====> Finally, the "row_l" list is appended into the "data_list" list to created a list for each row of data inside a list and the "data_list" that holds the lists of for each row of data is displayed to confirm that we do have a list of lists with each list being an individual row of data that matches each row from the table on the website
9) The results from "data_list" are then turned into a pandas dataframe called "mars_weather_df" and the column names are specified ('id','terrestrial_date','sol','ls','month','min_temp','pressure')
10) Next the data types of each column are changed to their respective data types that will be needed for analysis later in the code using ".astype()"  => 'id' = object, 'terrestrial_date' = datetime64[ns], 'sol' = int64, 'ls' = int64, 'month' = int64, 'min_temp' = float64, 'pressure' = float64 ===> Column data types are then checked again to confirm that they were converted correctly
11) Next is the analysis of the data that was extracted from the website starting with figuring out "How many months are there on Mars?" and then sorting the series by month with ".sort_index()"
12) The second analysis was "How many Martian days' worth of data are there?" which was done by using ".count()" on the "sol" column since a sol is one Martian day
13) The third analysis was "What is the average low temperature by month?" which was done by grouping the "mars_weather_df" by "months" and "min_temp" and then using the ".mean()" function to find the average minimum temperature by month and results were stored in a variable called "months_avg_low_temp" ==> The series was then sorted by months in ascending order
14) A bar chart was created to visualize the average temperature by month using 'the months_avg_low_temp' series => x and y-axis labels along with a title were added for better readability
15) A bar chart was then created to visualize the coldest and hottest months in Curiosity's location using 'the coldest_to_hottest_months' series => "coldest_to_hottest_months" series was created by sorting the "months_avg_low_temp" by temperature in ascending order to show the coldest to warmest month ==> x and y-axis labels along with a title were added for better readability
16) The fourth analysis was "What is the average pressure by Martian month?" which was done by grouping the "mars_weather_df" by "months" and "pressure" and then using the ".mean()" function to find the average atmospheric pressure by month and results were stored in a variable called "months_avg_pressure" ==> The series was then sorted by months in ascending order
17) A bar chart was then created to visualize the average atmospheric pressure by month using the 'lowest_to_highest_pressure_months' series => "lowest_to_highest_pressure_months" series was created by sorting the "months_avg_pressure" by pressure in ascending order to show the weakest to strongest atmospheric pressure month ==> x and y-axis labels along with a title were added for better readability
18) The last visualization that was created to visualize "How many terrestrial (earth) days are there in a Martian year?" which was done by defining the x-axis as the "sol" column from the "mars_weather_df" and the y-axis as the "min_temp" column from the "mars_weather_df" and then plotting the x and y axis values => x and y-axis labels along with a title were added for better readability
