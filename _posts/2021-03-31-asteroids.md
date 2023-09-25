---
layout: post
title: Asteroids
description: Data cleaning and preparation with pandas.
image:
---


## Data Cleaning and Preparation

### Summary
How much is an asteroid worth if we were to mine them? Are they close to earth? What is the diameter?

This project consisted of cleaning data from three different sources: a flat file, scraping a website, and connecting to an API. The cleaning of the data utilizes pandas DataFrame. The final product included joining all three sources on the same key by storing them in a SQLite database.

The final database contained information on asteroids, how much they would be worth if we were to mine them, and if they are a near earth object. The most challenging piece was creating a common key to join the data frames on. Each source used a slightly different nomenclature for naming the asteroids, which needed to be uniform to join them on the same key.

### Tools
* Pandas
* BeautifulSoup
* Sqlite3

### Highlights
* Scraping websites
* API database
* Missing value handling
* Feature creation
* Binning columns
* Changing column types
* Regular expressions to change text

### Project Preview
Preview of one DataFrame before cleaning and after cleaning. Column names were renamed, dollar value columns were changed from strings to integers, then binned into groups if they were worth millions, billions, or trillions of dollars.

#### Before
![Asteroids DF Before](/assets/images/asteroid_before.JPG)

#### After
![Asteroids DF After](/assets/images/asteroid_after.JPG)

### The Complete Project
<section id="Repository">
	<div class="inner">
    <ul class="actions fit small">
      <li><a href="https://github.com/Torreylee1028/Asteroids-Data-Preparation" target="_blank" class="button small">View Repository</a></li>
    </ul>
	</div>
</section>
