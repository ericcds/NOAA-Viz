# NOAA-Viz
Narrative Visualization using NOAA Severe Weather Data

#About the Data

##Dataset


The dataset was downloaded from NOAA (the National Oceanic and Atmospheric Association), which compiles a database of severe weather events dating back to 1950. Data is limited for certain timeframes: the time period from 1950 - 1954 records only Tornado events, and the time period from 1955 - 1995 records only Tornado, Thunderstorm, and Hail events. The period from 1996 - present records all severe weather events as gathered and described in <a href="https://www.ncdc.noaa.gov/stormevents/pd01016005curr.pdf">NWS Directive 10-1605</a>. There are 48 different types in total.

The complete dataset is available as a bulk data download from NOAA via FTP or HTTP at <a href="https://www.ncdc.noaa.gov/stormevents/ftp.jsp">NOAA via FTP or HTTP</a>. The data is contained in multiple GZip'd CSV files that are separated by year and content. Three types of files are available: Detail, Location, and Fatalities. For the purposes of this visualization we worked only with the data in the Detail files.

##Data Cleansing

The files were downloaded and extracted to a local folder using R, then they were concatenated into a single dataframe. During examination of the data it became apparent that there were some numeric values that were represented as characters (e.g. 10M for 10,000,000 or 1.25K for 1,250). These were converted to numeric values and multiplied by the appropriate multiplier.

##Filtering

Because of the different data collected during each of the time periods described above, I decided to limit the dataset to the years for which all event types were captured. The dataset was filtered to contain only data from 1996-2016. 2017 data is only available through March; it was removed as well.

Data was then filtered to exclude those storm events that resulted in no damage, no injuries, or no deaths. To further reduce the size of the dataset, the data was also pre-aggregated by year for use in trend charts.

##Categorization

While working with the data visually, it became clear that working with all the different event types recorded by NOAA was difficult. Some events were far more prevalent than others, making visualizations on the same scale difficult to resolve. I attempted to recategorize the data into some broader event category types, coming up with a final list of 16.

##Visualization<

The narrative structure chosen for this visualization is the martini glass. The narrative begins with a broad set of information, and then proceeds down an author-guided path that explores one way of investigating the data before allowing the user to investigate on his or her own.

We begin by looking at the different metrics we have available in the data. These are Total Deaths, Total Injuries, Total Damage, and Event Count. They are visualized as simple line charts in a trellis with a red line indicating the mean value for that metric.

There are a number of different trends we might see from this multi-faceted view, but for the author-guided narrative, we will focus on the Total Deaths metric.

The next visualization is a streamgraph showing Total Deaths over time for each of the event categories. The initial resolution is YearMonth, which results in a relatively busy streamgraph. There are clearly some spikes in deaths around particular years, but it’s a bit hard to get a sense of how they relate to the big picture with all the other noise around.

We step the view back, looking at the same streamgraph with a resolution of Year. In this visualization, there are clear indications of 3 time periods with unusually high death tolls.

Since there is once very clear uptick in deaths around 2005, we'll narrow in on that time range. The next chart shows just the events from January to December, 2005. With a big spike in casualties from Tropical Vortex events (Hurricanes, Typhoons, Tropical Storms, etc.) it is pretty clear what we're looking at. The uptick is directly related to Hurricane Katrina.

Finally we turn control back over to the user, allowing them to explore the data from a variety of perspectives. The freeform exploration uses parameters for the data element or metric the user wants to view, and changing the parameter causes a trigger to fire which dynamically changes the chart to reset the scale, axes, categories, lines, etc.

Each of the charts was embedded with Vega-Tooltips to provide a measure of interactivity during the slideshow. When hovering over any portion of the data, the tooltip displays relevant values contained in that datum. Additionally, in the interactive chart, hovering over a particular datum uses that point as a parameter, extracting the Event Category and Year values and dynamically updating the chart title as the user mouses over interactive elements.