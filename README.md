# Aviation Accident Analysis
 
## Overview
 
This project analyzes aviation accident data to help an airline and airplane insurer understand which aircraft are the safest once an accident happens. The client wants to know which makes and models have a low rate of total destruction and a low chance of serious or fatal injuries for the people on board. The client also wants to know which general conditions play a role in how severe an accident is.
 
## Business Problem
 
The client is only interested in professionally built airplanes that could still be in service. We assumed a maximum lifetime of 40 years, so we only kept accidents from 1983 onwards. The client also asked for separate recommendations for small airplanes and larger passenger airplanes. We used a threshold of 20 passengers to split the two groups. Throughout the analysis, we made sure that each claim is based on enough accidents to be reliable.
 
## The Role of Domain Knowledge
 
Domain knowledge was the most important part of this project. Before making decisions on the data, we did a lot of research on how aviation really works, so that our choices match reality and not only the numbers.
 
This research guided many steps of the analysis. We had to understand what the weather codes mean: VMC is flying with good visibility, while IMC is flying in clouds or poor visibility using instruments only. We had to understand the different phases of flight and why some of them, like maneuvering and climb, are more dangerous than others. We also learned that the same aircraft model can be written in many ways in the records, and that a label like "Boeing 737" without a version can group very different airplanes built over several decades. Finally, research helped us interpret the results. For example, some small aircraft such as the Ayres S2R-G10 and Grumman G164B are agricultural airplanes, which explains why they often carry only one person and why their results look different from other small airplanes.
 
Without this knowledge, we could have kept wrong values, merged the wrong categories or recommended aircraft based on results that do not make sense in the real world.
 
## Data
 
The data comes from the National Transportation Safety Board (NTSB) aviation accident database, which covers events from 1948 to 2023. After cleaning, the dataset contains 57,253 accidents, of which 56,598 involve small airplanes and 655 involve large airplanes.
 
## Data Cleaning
 
The cleaning work is in Aviation_Accidents_Cleaning.ipynb. We kept only airplanes that were not amateur built and only accidents from 1983 onwards. We cleaned the Make column so that the same manufacturer is not written in several ways, and we kept makes with at least 50 accidents. Since model labels are not unique across makes, we created a Make.Model column to identify each plane type.
 
We also created three key measures. Total.Passengers is the total number of people on board, estimated as the sum of fatal, serious, minor and uninjured people. Fatal.Serious.Fraction is the share of people on board who were seriously injured or killed. Destroyed is equal to 1 when the aircraft was destroyed and 0 otherwise, so its mean gives the destruction rate. The cleaned data is saved in data/AviationData_Cleaned.csv.
 
## Analysis
 
The analysis is in Aviation_Accidents_Data_Analysis.ipynb. We compared makes and plane types on the two measures the client cares about, then looked at how weather and phase of flight affect the outcome of an accident.
 
One important finding is that most accidents have a fatal/serious fraction of 0, while a smaller group has a fraction of 1, where everyone on board is seriously hurt or killed. The median is 0 for the best makes, so the mean is pulled up by a few very severe accidents. We also saw that some large makes have only 1 to 5 accidents, so their low rates are not reliable and we did not recommend them.
 
## Recommendations
 
*Small airplanes.* The average for small airplanes is 27.3% for fatal/serious injuries and 21.1% for destruction. WACO, Maule, Helio, Aviat Aircraft Inc and Great Lakes are well below this average on both measures. Maule is the strongest choice because its result is based on 567 accidents, with 15.4% injuries and 9.3% destruction. At the model level, the Piper PA-18A 150, Diamond DA 20 C1, Maule MX-7-235, Maule M-7-235B, Cessna C172 and Beech 1900D perform well on both measures.
 
*Large airplanes.* The average for large airplanes is 14.3% for fatal/serious injuries and 17.1% for destruction. McDonnell Douglas (6.2% injuries) and Bombardier (7.1% destruction) are clearly below average on both measures. Boeing is close to average but, with 316 accidents, it is the most reliable result in this group. At the model level, the McDonnell Douglas MD-88 and the Bombardier CL-600-2B19 stand out, with almost no serious injuries and no aircraft destroyed, followed by the Boeing 737-300.
 
## Factors Affecting Accident Severity
 
*Weather condition.* In good visibility (VMC), the mean fatal/serious fraction is 22.3% and 16.8% of aircraft are destroyed. In poor visibility (IMC), these numbers jump to 67.7% and 59.4%. An accident in poor visibility is about three times more likely to be severe. Both groups have thousands of accidents, so this result is robust.
 
*Phase of flight.* Accidents during taxi and landing are the least severe, with less than 5% fatal/serious injuries and less than 5% destroyed. Maneuvering is the most dangerous phase, with 53.0% fatal/serious injuries and 47.4% destroyed, followed by climb, approach, cruise and descent. Landing accidents are frequent but mild, while maneuvering and climb accidents are less frequent but much more severe.
 
## Limitations
 
The large-airplane group is small (655 accidents), and each plane type has only 10 to 52 accidents, so these results should be read with caution. Also, our measures describe how severe an accident is once it happens. They do not show how often each make has accidents, because the data does not include the number of flights or flight hours.
 
## Repository Structure
 

├── data/
│   ├── AviationData.csv
│   ├── AviationData_Cleaned.csv
│   └── USState_Codes.csv
├── Aviation_Accidents_Cleaning.ipynb
├── Aviation_Accidents_Data_Analysis.ipynb
├── LICENSE
└── README.md

