# WeatherPy And Vacation Planning

## Overview of Project

### Purpose

This project focuses on making use of both Google Maps API and OpenWeatherMap API to determine recent weather in order to plan out a vacation itinerary dependent on the ideal temperatures of the user. The act of which is split into three sections: Retrieving weather data from OpenWeatherMap, retrieving the nearest hotels from Google Maps and plotting the most ideal locations on a map, and determining a rudimentary vacation itinerary from a starting point and three accessory points that loop back to the starting point when moved between.

## Results

### Retrieving Weather Data with OpenWeatherMap

The first step is to retrieve weather data from OpenWeatherMap through their API. We produced a random list of 2000 tuples via normal distribution that correspond to readable latitude and longitude pairs. By using Citipy, a Python module, we can determine the closest city to each latitude-longitude pair, and use the resulting city and country values in OpenWeatherMap's API to get weather conditions for that city, including a general statement, wind speeds, and maximum temperature, as well as the true latitude and longitude for that city, which we compile into a single DataFrame. Because of the possibility of repeat cities, the DataFrame we produce is not necessarily 2,000 entries large, though it might be possible with sufficient distribution that the Dataframe can be that large.

### Determining Ideal Locations and Nearest Hotels

The second step is to determine which locations would be ideal to go to for vacation and to determine hotels closest to each locale. Because there is no single preferred temperature range among everyone, this is left into input. We decided that, for personal reasons, we input a range of 10F to 55F, although any temperature range would suffice. Next, we'd select only cities whose max temp was within the range specified, and clean the data to make sure there are no null values, putting them into a new DataFrame with an additional tab to account for hotels. From there, we comb through the cities listed and attempt to find hotels for each city listed, adding them onto the DataFrame, and any that we can't find a hotel for we remove from the DataFrame.

When put onto a map, the following is what is produced:

![alt text](https://raw.githubusercontent.com/SirNancyTheNegative/World_Weather_Analysis/main/Vacation_Search/WeatherPy_vacation_map.png "The DataFrame's entries being put onto a world map")

Because we specified particularly low temperatures, we get results that, expectedly, are further from the equator. If we specifically selected higher temperatures, we would get results that were closer to the equator, as well as more landlocked results. Conversely, if we see results in the southern hemisphere for colder temperatures, the time we would see the most results would be around June through August, when those countries would be going into winter.

### Finalizing an Itinerary

Now that we have a vizualization of the cities that fit our criteria, we need to determine how the itinerary should be laid out. We decided on three stops forming a loop from one main location, starting at Rapid Valley, SD, and going through Sheridan , WY; Golden, CO; and Council Bluffs, IO, before returning to Rapid Valley. All of this travel would be done by car. Use of the Google Directions API is set up as to feasibly use the direction of the streets to map out the travel. Planning out this trip, the circuit would look like this:

![alt text](https://raw.githubusercontent.com/SirNancyTheNegative/World_Weather_Analysis/main/Vacation_Itinerary/WeatherPy_travel_map.png "A circuit starting from South Dakota, going through Wyoming, Colorado, Nebraska, and Iowa before returning to South Dakota")

As can be seen, the Google Directions API maps out the path that one might take if going from one city to another using a GPS app, instead letting us get a gist of the path taken to fulfill the itinerary. However, in this form, we don't get to see the destination we really care about -- the hotel is nowhere to be seen in the marker blurb.

What we can do, then, is take those four points we used to make the path, and add only those to a new DataFrame. In doing so, we can repeat what we did when we mapped each and every ideal city onto a map. In doing so, we produce this map:

![alt text](https://raw.githubusercontent.com/SirNancyTheNegative/World_Weather_Analysis/main/Vacation_Itinerary/WeatherPy_travel_map_markers.png "Our four destinations singled out on the map")

With these, we now know where we need to end up as the legs of the journey progress.

## Summary

### The Vacation

A few weeks ago, if we wanted to plan out a vacation in a particular area, we'd have to painstakingly figure out areas that are nice this time of year, consider how best to get there, and have to manually see what's around the area in order to have a vacation. With the use of APIs, however, we can take a broad view of the world, find a comfortable climate with ideal temperatures, pick a spot on the world map we'd like to visit, pick some nearby areas to explore, and build a simple itinerary off of that alone. While this system isn't perfect, it is far more efficient than painstakingly checking the weather piecemeal until we find a vacation locale that suits our desires before we can even consider an itinerary. With these programs, we can whittle down that process into a matter of pushing a single button a few times, making a few short selections, and spending the time in the interim considering the overall goal of the vacation.