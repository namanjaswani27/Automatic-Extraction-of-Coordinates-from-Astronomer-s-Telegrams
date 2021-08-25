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

  
