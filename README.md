## Team Members
Caleb Rivers (https://github.com/CRivers2805/MIST_4610_21482_G5_CMR) 

Catherine Lusick (https://github.com/cl95728/MIST-4610-Group-5-Project-1) 

Emmy Nguyen (https://github.com/emmyn1/MIST-4610-Group-5-1)   

Diyaa Patel (https://github.com/Diyaa-P13/MIST4610---Project-1-Group-5.git)   

# Project Description
The purpose of this relational database is to model a music group that distributes songs and albums from a variety of different artists that are signed to various subsidiary record labels. The model tracks artists, albums, songs, record labels, contracts, and revenue generated through both streaming and unit sales, with the central entity being the artists, as their products are the source of revenue.  Managers can use the system to assess artist performance, identify high-performing genres and locations, and make strategic choices about talent acquisition, contract management, and marketing. Through querying the database, our team aims to prove that our database is both reliable and useful for helping the executive team gain insight into the current operations of the music group, as well as ensuring that it can be used to make decisions about the future of the firm.

# Data Model Description
The database features the entities Record Label, Location, Artist, Contract, Album, Song, Artist group, Producer, Song Producer, Total Units, Streams Total, and Sales.

Record Label represents the subsidiary that each artist is signed to. It is the child table of location, as a location could include many record labels. Other attributes include the albums unique identifier, it’s name, the city in which it is headquartered in, and the year it was founded.

Location represents the relevant areas that house producers, record labels, and artists. Since none of these entities can have more than one location, the entity has no foreign keys. A locations state, city, and ZIP code is represented in the model.

The artist is the core entity, and has relations with the most amount of other entities in the database. An artist’s attributes include their unique identifier, their stage and legal name, the date of their first album release, their age, and foreign keys connecting them to location and record label, as record labels and locations can have multiple artists. The Artist entity includes both artists that belong to our client’s music group, as well as artists beyond the music group that their artists have collaborated with.

An artist’s contract outlines what they are required to do in order for their respective labels to promote and distribute their music. Each contract has their unique identifier, their start and end date, the percent of every dollar that the artist gets to keep, the amount of their initial advances, and the amount of albums the artist is required to produce before their contract expertise. Lastly, the only foreign key included is artist ID, as every artist we are observing needs a contract, but not every artist in general has a contact with this specific music group, such as feature artists, which are also included in the model.

The Album is a sum of songs that are released at one time, and are used to fill contracts by the artists. Albums have their unique identifier which is a combination of artist ID and the release of the album, and are described by their name and their release date. Their foreign keys link them to artist and units sold, as artists can have multiple albums, and multiple albums can have the same amount of units sold.

Albums are composed of songs, which is also an essential entity in our model. Songs serve as the core product in the form of streams (along with physical vinyl sales), and are essential in determining revenue metrics. Each song has a unique identifier, which is a combination of artist ID, album ID, and the track number of the song. Other attributes include the song name, runtime, genre, and maturity rating, each essential features that can affect the revenue of a track. Foreign keys compose of album ID and stream total, as an album has many songs, and multiple songs can have the same amount of streams.

Artist Group represents the associative entity between songs and artists, as an artist can have many songs, and an undeniably have many songs, and a song can also have many artists working on it. To accurately model this relationship, we implemented a three-way composite primary key, with each row having a unique combination of group ID, artist ID, and song ID. The only other attribute that is attributed to this entity is group name, which describes each artist that works on a song in one cell.

In addition to an artist, each song also has a producer that composes the instrumentals and mixes the track. Producer is modeled similarly to artist, with producer ID, producer name, and producer age as it’s independent attributes, and location ID as its foreign key

Similarly to artists, a producer can work on many songs, and a song can also be composed by many producers. As such, another associative entity, song producer, was made to represent this relationship. The only attributes are its three-way composite primary key consisting of song producer ID, producer ID, and song ID

The Unit Total Entity was created to represent the amount of physical media (i.e. vinyl and CDs) that an album sells throughout its lifetime. This entity is composed of its unique identifier, the total quantity of units that an album has sold, and a foreign key linking the table to sales, which will be expanded upon below.

Streams is another avenue for an artist to generate revenue, so this is also modeled in its own entity. However, unlike being related to albums like units total, streams is related to songs, since people can stream songs individually and do not have to listen to an entire album for a stream to register. Streams include a unique identifier, the total quantity of streams generated, and the foreign key linking this entity to sales.

Lastly, but perhaps most essential, is sales. This is the table that holds the revenue generated from both units sold and streams. Although a relatively simple table, sales offer the most critical data that is found in the database, and can offer the most insight as to what direction the firm needs to move in. Despite only consisting of a unique identifier and the revenue generated by each distribution channel, it is used in many of our queries to determine which artists prove to be most valuable.

<img width="468" height="470" alt="image" src="https://github.com/user-attachments/assets/71f0b386-c771-482f-ae5a-06119d235188" />

# Data Dictionary
### Artist Table
| Column Name | Data Type | Description |
|------------|----------|------------|
| artistID | INT | Unique identifier for each artist |
| legalName | VARCHAR | Artist's legal name | 
| stageName | VARCHAR | Artist's stage name |
| debutDate | INT | Year that artist debuted | 
| artistAge | INT | Current age of the artist | 
| locationID | INT | References the artist's location | 
| recordLabelID | INT | Foreign key referencing the record label associated with the artist |

### Artist Group
| Column Name | Data Type | Description |
|------------|----------|------------|
| groupID | INT | Unique identifier for a collaboration group involving multiple artists on a song |
| artistID | INT | Foreign key referencing an artist participating in the group | 
| songID | INT | Foreign key referencing the song associated with the group collaboration | 
| groupName | VARCHAR | Name of the artist group or collaboration | 

### Location
| Column Name | Data Type | Description |
|------------|----------|------------|
| locationID | INT | Unique identifier for each location | 
| state | VARCHAR | State abbreviation where the location is based | 
| city | VARCHAR | City name of the location | 
| zipCode | INT | ZIP code associated with the location | 

### Contract
| Column Name | Data Type | Description |
|------------|----------|------------|
| contractID | INT | Unique identifier for each contract | 
| startDate | DATE | Date the contract begins | 
| endDate | DATE | Date the contract ends | 
| royaltyRate | DECIMAL | Percentage of revenue paid to the artist | 
| advanceAmount | DECIMAL | Upfront payment given to the artist | 
| albumQty | INT | Number of albums required under the contract | 
| artistID | INT | Foreign key referencing the artist associated with the contract | 

### Record Label
| Column Name | Data Type | Description |
|------------|----------|------------|
| recordLabelID | INT | Unique identifier for each record label | 
| labelName | VARCHAR | Name of the record label | 
| hqCity | VARCHAR | City where the laebl is headquartered | 
| yearFounded | INT | Year the record label was established | 
| locationID | INT | Foreign key referencing the location of the record label | 

### Album 
| Column Name | Data Type | Description |
|------------|----------|------------|
| albumID | INT | Unique identifier for each album | 
| albumName | VARCHAR | Name/title of the album | 
| releaseDate | DATE | Date of the album was released | 
| artistID | INT | Foreign key referencing the artist who created the album | 
| unitsSoldID | INT | Foreign key referencing the units sold record associated with the album | 

### Song 
| Column Name | Data Type | Description |
|------------|----------|------------|
| songID | INT | Unique identifier for each song |
| songTitle | VARCHAR | Title of the song | 
| songDuration | VARCHAR | Duration of the song in minutes and seconds | 
| songGenre | VARCHAR | Genre classification of the song | 
| explicit | VARCHAR | Indicates whether the song contains explicit content (Yes/No) |
| trackNumber | INT | Position of the song within the album | 
| albumID | INT | Foreign key referencing the album the song belongs to | 
| streamTotalID | INT | Foreign key referencing the total streaming data for the song | 

### Producer
|Column Name | Data Type | Description |
|------------|----------|------------|
| producerID | INT | Unique identifier for each producer | 
| producerName | VARCHAR | Name of the music producer | 
| producerAge | INT | Age of the producer | 
| locationID | INT | Foreign key referencing where the producer is based in | 

### Song Producer 
|Column Name | Data Type | Description |
|------------|----------|------------|
| songProducerID | INT | Unique identifier for each song-producer relationship |
| producerID | INT | Foreign key referencing the producer associated with the song | 
| songID | INT | Foreign key referencing the song associated with the producer | 

### Sales
|Column Name | Data Type | Description |
|------------|----------|------------|
| salesID | INT | Unique identifier for each sales record | 
| revenueAmount | DECIMAL | Total revenue generated from sales |

# Queries

## Query Checklist
| Feature                   | Query 1 | Query 2 | Query 3 | Query 4 | Query 5 | Query 6 | Query 7 | Query 8 | Query 9 | Query 10 | 
|---------------------------|---------|---------|---------|---------|---------|---------|---------|---------|---------|----------|
| Multiple Table Join       |         |    X    |    X    |    X    |    X    |    X    |    X    |    X    |         |     X    |
| Subquery                  |         |         |         |         |         |         |         |    X    |         |          |
| GROUP BY                  |         |         |         |         |    X    |         |    X    |    X    |         |          |
| GROUP BY with HAVING      |         |         |         |    X    |         |         |         |         |         |          |
| Multi-condition WHERE     |         |         |    X    |         |         |         |         |         |         |          |
| Built - in Functions      |         |    X    |    X    |    X    |    X    |    X    |    X    |    X    |         |          |
| REGEXP                    |         |         |         |         |         |    X    |         |         |    X    |          | 
| NOT EXISTS                |         |         |         |         |         |         |         |         |         |     X    |
| WHERE Clause              |    X    |         |         |    X    |         |    X    |         |         |         |          |
| Basic SELECT              |    X    |    X    |    X    |    X    |    X    |    X    |    X    |    X    |    X    |     X    |
| Union                     |         |         |         |         |         |    X    |         |         |         |          |

## Query 1 - What are all of Dolly Parton's albums?
this query retrieves album names and release dates for a specific artist by filtering the Album table using the artist’s ID. It provides a simple view of Dolly's discography. This query gives management quick access to an her portfolio of work and track her release history. Understanding an artist’s output is important for planning future releases and activities. It also provides an idea of an artist’s content production and an overview of their career progression.

<img width="274" height="262" alt="image" src="https://github.com/user-attachments/assets/18678b8d-4208-4d96-9fe3-c19103f8e16e" />

## Query 2 - What song has been streamed the most?
This query retrieves song titles and their total stream counts by joining the Song and Stream Total tables. It ranks songs in descending order and returns the top 10 most-streamed tracks. This query allows management to have a better understanding of which songs are currently the most popular among listeners. High streaming numbers indicate strong audience engagement and can guide the company’s promotion decisions. The results can also be utilized to maximize revenues from streaming platforms.

<img width="385" height="275" alt="image" src="https://github.com/user-attachments/assets/3b44073a-9af4-4654-94ed-a916f3f73365" />

## Query 3 - Which albums have sold at least 900,000 units?
This query retrieves album names and total units sold by joining Album and Unit Total tables. It filters for albums exceeding 9,000,000 units and orders them from highest to lowest sales. This query helps management identify which albums are performing well in terms of sales volume. By focusing on high-selling albums, the label can prioritize its resources for the successful projects. This insight can guide future investment strategies and production decisions.

<img width="318" height="293" alt="image" src="https://github.com/user-attachments/assets/be8230e5-d055-4e7c-bbd5-d21347265803" />

## Query 4 - Which Hip Hop group gets the most streams per collaboration?
This query is meant to identify which hip hop group feature generates the largest number of streams. Some groups have multiple collaborations, so for more accurate results, the total streams earned by each group are divided by the number of songs they have in the database. As shown in the results, J Cole and Trey Songz have garnered the most streams per song, so it would be wise to get both artists back into the studio to produce another hit. Additionally, JID’s features make up most of the top 50%, so he seems to work well with other artists. Lastly, Kendrick Lamar’s features tend to lack streams, so maybe the label should encourage him to stick to solo work.

<img width="468" height="223" alt="image" src="https://github.com/user-attachments/assets/5717df9c-c083-4913-9f3e-a93cecc78039" />

## Query 5 - Where should we look for new talent?
This query is meant to give insight on which cities generate the most revenue per artist. By joining many tables across the database, we can attach revenue values to all of the locations in our database. Additionally, dividing by artist creates less skewed data, as the cities with more artists will not be overrepresented. As seen in the results, Chapel Hill, Duluth, Houston, and Charleston have shown massive returns for their respective artists, so perhaps the culture and connections these artists can create in their cities can allow for similar artists from their area to develop and follow in their footsteps. Therefore, more resources should be given to talent scouts and local development in those areas.

<img width="411" height="255" alt="image" src="https://github.com/user-attachments/assets/459a5743-b6ab-433e-8a4f-f717351203ab" />

## Query 6 - Do pre- or post-2000s albums generate the most revenue?
This query displays the dichotomy of the revenue generated from albums before and after the year 2000. By using the UNION command, we can observe both calculations side by side. REGEXP was used to distinguish between albums made before and after the turn of the millennium. The results state that pre-2000s albums still have generated more money per album on average than post 2000s albums. This should alert management that they need to keep these albums available for purchase and to not phase them out. It would also be wise to renew contracts of artists that made music in the 1900s, as they not only drove up sales, but they have a positive reputation amongst the public. This isn’t to say that newer artists should not be prioritized, as their sales numbers are very close to those of the older albums, however management should not ignore the lasting impact that older works have created.

<img width="468" height="217" alt="image" src="https://github.com/user-attachments/assets/07444e8d-f7ee-4abe-af67-8c34285c0b6d" />

## Query 7 - Which record label has released the most albums?
This query calculates the total number of albums released by each record label by joining the Album, Artist, and Record Label tables. It organizes the data by record label and counts the number of albums linked to each label, and then it arranges the results in descending order. This query assists management in determining which record labels are generating the most albums. Being able to identify which label is effectively, provides insight into overall label performance and market presence. This data can help make decisions about investments, resource distribution, and collaborations with successful labels.

<img width="285" height="280" alt="image" src="https://github.com/user-attachments/assets/e60334a7-6a71-4048-83e7-ee9d29328c1e" />

## Query 8 - Which artists have more total album sales than the average album sales of all artists?
This query calculates the total album sales for each artist by joining the Artist, Album, and Unit total tables. By comparing, each artist’s total sales to the average total sales across all artists using a subquery, it returns only those artists whose sales are higher than the average. This query assists management in determining artists who are exceeding average sales performance. These insights can help make decisions regarding marketing spending, resource distribution, contract extensions, and focusing on top-performing artists within the company.

<img width="222" height="194" alt="image" src="https://github.com/user-attachments/assets/1259c45d-6f32-4441-90d5-2231cce4c75d" />
<img width="208" height="195" alt="image" src="https://github.com/user-attachments/assets/66ec1872-4e6d-401e-9caa-0c8da75a7bed" />

## Query 9 - Which locations have a city that ends in "-ville"?
Query 9 was created to pull a list of all cities in the Location table that ends with the letters "ville". To make the list clean and easy to read, we used a Regular Expression to find the pattern and grouped the results by city. This query helps filter through the location data more effectively. Instead of scrolling through rows of data, this helps identify specific areas based on their name. As seen in certain types of music, artists frequently shorten the name of their cities, for example, referring to Fayetteville as "The Ville". With this analysis, we can potentially market to other areas that include "-ville" to increase a sense of familiarity with the music.

<img width="293" height="194" alt="image" src="https://github.com/user-attachments/assets/4e1fde89-8ff8-449d-986d-08418f979e9b" />

## Query 10 - Which producers have yet to work on a Hip Hop song?
Query 10 is designed to find the names of producers in the Producer table who have never been associated with a "Hip Hop" song. To do this, we used a NOT EXISTS subquery to filter anyone linked to that specific genre. For every producer, the subquery checks the Song Producer table to see if they are linked to any song labeled 'Hip Hop'. If the subquery finds any match, NOT EXISTS becomes false, and that producer is excluded. This logic can be used to isolate producers who work exclusively in other genres like Country or Pop. It’s a great way to find a music producer whose specialty does not fall in Hip Hop if an analyst is not concerned with that genre.

<img width="266" height="173" alt="image" src="https://github.com/user-attachments/assets/d40ec457-831c-4426-ab60-9a19816b2548" />

# Database Information
Name of the database: al_Group_21482_G5
