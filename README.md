# Automatic-Extraction-of-Coordinates-from-Astronomer-s-Telegrams

# Introduction
The [Astronomer's Telegram (ATel)](https://www.astronomerstelegram.org) is an internet based short notice publication service for quickly disseminating information on new astronomical observations. Telegrams are available instantly on the service's website and distributed to subscribers via email digest within 24 hour.

# Problem Description
The project aims at **extracting the location** of the observed objects from astronomy circulars in an
automated way. This would be used to create an interface to query all the circulars which referred
to a particular location.

The location of any object in the sky is given by a pair of coordinates called `right ascension (R.A)`
and `declination (Dec.)`. Just as every point on the surface of the earth can be specified using its
latitude and longitude, every point in the sky is specified by its right ascension and declination. The
*right ascension* corresponds to the longitude and can be specified in either `degrees (0 to 360)` or
`hours (0 to 24)`. The *declination* corresponds to the latitude and is specified in `degrees (-90 to 90)`.
There are many intricacies about the astronomical coordinates but they are not relevant from the
point of this problem statement.

The input is the text content of the ATel, from which we want to extract coordinates information,
and the output is a set of coordinate pairs from that ATel.

# Why not use Regex ( Regular Expression )
- ***False positive** with date-time* : 'INTEGRAL performed a target-of-opportunity observation of the colliding wind binary eta Carinae from 2019-12-06 13:10:19 to 2019-12-07 09:28:36 (UTC)'
- *Extracting coordinates in **decimal format*** : ‘Object TXS 0358+210 with radio
coordinates (J2000) R.A.: 60.43819 deg, Dec.: 21.17461 deg (Beasley et al.
2002, ApJS 141, 13’
- ***False positive** in Object name format* : ‘We obtained optical spectra covering the
range 5000-9400 A with the 3.58m TNG telescope equipped with LRS at
Observatorio del Roque de los Muchachos’

# Approach

1. Apply regex to extract coordinates with Object-name-format. If found, then just keep it, else step 2 onwards.
2. Trained a Linear classifier (SVM on TFIDF of input documents) on sentences containing all formats except Object-name-format and Decimal-format.
3. During inference, if sentence is labeled as '1', then apply regex to extract all formats except Object-name-format and Decimal-format. 
4. If regex did not extract any coordinate, then that means sentence containes coordinates in Decimal-format. Hence apply regex to extract Decimal-format

![Approach](https://github.com/namanjaswani27/Automatic_Extraction_of_Coordinates_from_Astronomers_Telegrams/blob/main/Model_Pipeline.png?raw=true)

# Results [ on Validation data ]

## Classifier : `SVM`

`Classification Scores `
| Class | Precision | Recall | F1 Score | Support |
| :---: | :---: | :---: |  :---: | :---: |
| 0 | 0.96 | 0.95 | 0.96 | 145 |
| 1 | 0.94 | 0.95 | 0.95 | 125 |

`Confusion Matrix`
||Actual Positive| Actual Negative|
|:---:| :---: | :---: |
|Predicted Positive| 119 | 7 | 
|Predicted Negative| 6 | 138 | 


## Classifier : `Logistic Regression`

`Classification Scores `
| Class | Precision | Recall | F1 Score | Support |
| :---: | :---: | :---: |  :---: | :---: |
| 0 | 0.99 | 0.95 | 0.97 | 145 |
| 1 | 0.95 | 0.98 | 0.96 | 125 |

`Confusion Matrix`
||Actual Positive| Actual Negative|
|:---:| :---: | :---: |
|Predicted Positive| 123 | 7 | 
|Predicted Negative| 2 | 138 | 




