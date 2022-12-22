# May Mobility (Data Scientist)

### README.md <!-- omit from toc -->

Date: 15 Dec 2022

## Table of Contents

- [May Mobility (Data Scientist)](#may-mobility-data-scientist)
  - [Table of Contents](#table-of-contents)
  - [Jesus R. Rosila Mares](#jesus-r-rosila-mares)
- [Take Home Exercise (Data Scientist)](#take-home-exercise-data-scientist)
  - [Questions](#questions)
    - [*Question 1*: EDA](#question-1-eda)
    - [*Question 2*: Data Insights](#question-2-data-insights)
    - [*Question 3*: Modeling I](#question-3-modeling-i)
    - [*Question 4*: Modeling II](#question-4-modeling-ii)
  - [Appendix](#appendix)

---

## Jesus R. Rosila Mares

- [GitHub Profile](https://github.com/jrosilam)

- [Linkedin Profile](https://www.linkedin.com/in/jrosilam/)

- [Data Scientist Resume](https://drive.google.com/file/d/1zrlaanzFNzdh1nAFth_IemuxQ-BZQJy6/view?usp=sharing)

- [Systems Engineer Resume](https://drive.google.com/file/d/12JxFKRkWKeZhiTGysg-ds-w4QnoOhId8/view?usp=sharing)

- [CV](https://drive.google.com/file/d/1YDn7v4gwnVJQ-2RTDxf-ftHEQFYteEEJ/view?usp=sharing)

# Take Home Exercise (Data Scientist)

We expect this exercise to take approximately 3-4 hours. Please read the entire document before
starting. Provided with the exercise are two datasets: *`site_ridership.csv`* and *`pickups.csv`*.
May Mobility has multiple operational sites around the world. One of the operational metrics we are
interested in is our ridership numbers. In this exercise, we provide some ridership data we collect
manually at one of our sites. The site is a circulator route meaning that it operates like a bus service
going around in a loop during service hours. Riders hop on and off the vehicle just like a bus service
and that information is recorded manually by site staff using Google Forms.

Additional information:

- Each vehicle is only allowed one household at a time in the vehicle. There is no ride sharing at this site.
- Each vehicle can hold up to a max of 4 riders in a household.
- Service hours are 7am - 7pm.

The dataset file *`site_ridership.csv`* consists of the following columns (all columns are manually entered
in the Google Form except for timestamp):

- timestamp (timestamp when Google Form is submitted)
- pickup (number of riders picked up)
- dropoff (number of riders dropped off)
- stop (stop name)
- vehicle (vehicle id)
- time (approximate time of pickup)
- date (date of pickup)
- name (initials of person filling out google form)

The dataset file *`pickups.csv`* consists of the same columns as *`site_ridership.csv`* with the addition of:

- row_id (row unique identifier)

> Please return an output file with the answers to the following questions. Also please provide
the code with comments in a script or notebook that was used to answer the questions.
Please provide any necessary commentary about what you are doing and why.

**Note:** State any assumptions you make about the data in your solution that was not already given in
the question.

## Questions

### *Question 1*: EDA

> Perform an EDA and provide a summary of the data (specifically *`site_ridership.csv`*). Target the most
important features of the dataset first. Does the dataset match your expectations?

See attached Notebook `takehome_test.ipynb` for plots and graphs.

The Services were provided around Purdue University in West Lafayette, Indiana.

Service does not run durring weekends.

Data set was collected between The dates: Jun 03 2021 to Oct 29 2021.

Errors included missing values, input errors of droping off 8 people when the max is 4, and operating outside of established hours.

Stats:

Missing pickup data:   12 out of 4352 records, 0.28%.  
Missing dropoff data:  15 out of 4352 records, 0.34%.  
Total null data:       27 out of 4352 records, 0.62%.  
Entry error data:       4 out of 4352 records, 0.09%.  
Total errors are:      31 out of 4352 records, 0.71%.  

The messed-up days range, could include from: June 17 2021 to June 22 2021.
| name | percent_error | errors | records |
| :--- | :-----------: | -----: | ------: |
| JR   |     0.39%     |      6 |    1557 |
| CM   |     1.20%     |     18 |    1497 |
| MV   |     4.17%     |      2 |      48 |
| LA   |     6.06%     |      2 |      33 |
| MN   |    25.00%     |      2 |       8 |
| HK   |    25.00%     |      1 |       4 |

There are 5 days that don't match pickup to dropoffs.  
| date       | pickup | dropoff |
| :--------- | -----: | ------: |
| 2021-06-24 |  11.00 |   10.00 |
| 2021-06-25 |   7.00 |    8.00 |
| 2021-07-14 |  21.00 |   20.00 |
| 2021-07-21 |  23.00 |   22.00 |
| 2021-10-01 |  44.00 |   46.00 |

Freq of both pickup and dropoff: 74 out of 4352, 1.70%
| freq      |  day |
| :-------- | ---: |
| Monday    |   18 |
| Tuesday   |   13 |
| Wednesday |   11 |
| Thursday  |   19 |
| Friday    |   13 |
| Saturday  |    0 |
| Sunday    |    0 |

A total of 10 entries recorded before 7am: 3 pickups and 7 dropoffs.  
A total of  1 entry recorded after 7pm: 0 pickups and 1 dropoffs.  

| hour | pickup | dropoff |
| :--- | -----: | ------: |
| 6    |      7 |       3 |
| 7    |    105 |      96 |
| 8    |    208 |     203 |
| 9    |    177 |     173 |
| 10   |    201 |     189 |
| 11   |    291 |     280 |
| 12   |    202 |     220 |
| 13   |    239 |     230 |
| 14   |    269 |     262 |
| 15   |    195 |     204 |
| 16   |    250 |     241 |
| 17   |    271 |     278 |
| 18   |    262 |     285 |
| 19   |     13 |      25 |
| 20   |      0 |       1 |

### *Question 2*: Data Insights

> Are there any data insights that you can provide that would be of interest to stakeholders of the
site/company? Feel free to add a plot for clarity if you think it is needed.

The Services were provided around Purdue University in West Lafayette, Indiana.

Service does not run durring weekends.

Data set was collected between The dates: Jun 03 2021 to Oct 29 2021.

Errors included missing values, input errors of droping off 8 people when the max is 4, and operating outside of established hours.

### *Question 3*: Modeling I

> Suppose the site team wants to predict what the ridership will be in the future for planning purposes.
Return a prediction about what the ridership will be on these dates **Nov. 15-21**. In the commentary, tell
us how well you think your model will do.

> Submit a comma delimited file called *`riders.csv`* with the following 2 columns:

```terminal
date,riders
Nov 15,<your prediction>
Nov 16,<your prediction>
…
Nov 21,<your prediction>
```

> We will use *`riders.csv`* on a private test dataset to see how well your model does.

More info and pretty plots in the Notebook under "Machine Learning I"  
From inital inspection and scatter plots, it looks like my Linear Model is good. But there is pitfalls with it predicting rides over the weekend and not extrapolating to the month of November. Accuracies, test/train splits, and plots found in the notebook.

### *Question 4*: Modeling II

> Suppose for some unknown reason, during the month of November, the site team only entered pickup
data. We would like to fill out this dataset by predicting where the associated dropoff locations are.
Predict the dropoff stop based on the input file *`pickups.csv`*. In the commentary, tell us how well you
think your model will do.    

> Submit a comma delimited file called *`dropoff.csv`* with the following 2 columns:

```terminal
row_id,dropoff_stop
1,<your prediction>
2,<your prediction>
…
363,<your prediction>
```

> We will use *`dropoff.csv`* on a private test dataset to see how well your model does.

More info and pretty plots in the Notebook under "Machine Learning II"

My approach for the Machine Learing algorithm is missing a counter to figure out average amount of stops before a dropoff is triggered. Which make an issue in the predictor being stuck in a singularity. There is a Pareto chart showing the percentage where dropoffs are triggered. As well as a confusion matrix chart that would be better if the machine learning was corrected. Need to review. Accuracies, test/train splits, and plots found in the notebook.

---

## Appendix

The table contains descriptions of the 9 route stops for some context.

| Stop       |           Description            | Latitude | Longitude |
| :--------- | :------------------------------: | -------- | --------- |
| Bus        | Bus stop on a major transit line | 39.77285 | -86.16168 |
| Dentist    |       School of Dentistry        | 39.77467 | -86.17895 |
| Doctor     |      Pediatrician’s office       | 39.77926 | -86.17496 |
| Admin      |     Administrative building      | 39.77459 | -86.17433 |
| Hospital   |         Campus hospital          | 39.77567 | -86.17557 |
| Lime       |        Bus stop on campus        | 39.77473 | -86.18376 |
| Parking    |        Campus parking lot        | 39.77882 | -86.18121 |
| School     |     School of Art and Design     | 39.77148 | -86.17148 |
| University |     University lecture hall      | 39.77271 | -86.17575 |