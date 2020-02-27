# Cluster Analysis at Duke University for Median Graduation Time Across Doctorate Programs

![alt text](https://gradschool.duke.edu/sites/all/themes/grad/logo.png)

## Determining Which Doctorate Programs are Conducive to Fast Graduation Times Across Gender

Doctorate programs are large time investments, and for students who are trying to decide between different life science programs of study, time until graduation may be an important deciding factor. Clsuter analysis was performed for all doctorate programs at Duke University with regard to program, time to completion, and gender. Analysis shows that across the three clusters of doctorate programs related to their length of copmletion, men take significnalty shorter amounts of time to earn their degrees in programs that are relatively fast as well as those that take relatively longer amounts of time than others. 

## Which Doctorate Programs Would be Best for Men and Women Who Want to Start Working Sooner

Doctorate programs are typically advertised as requiring 4 years of work, but according to [this article](https://www.usnews.com/education/best-graduate-schools/articles/2019-08-12/how-long-does-it-take-to-get-a-phd-degree-and-should-you-get-one) the actual medial time to complete a doctorate program in the United States is 5.8 years, and often takes longer. For students who want to earn a doctorate degree but wish not to spend too much time on it, and who may want to move on with their lives by getting a job and finally earning an income, time to graduation can be a very important consideration when choosing a program. Additionally, as the average age of earning the degree is 33 years old, and is around the time many people consider having children, it would be valuable to see if there is a significant difference between the length of time for men and women to earn the degree.

## How to Analyze Public Data from Duke University 

Data was collected from the Duke University section of the [Next Generation Life Science Coalition](https://nglscoalition.org/coalition-data/) website. Separate [raw PDFs](https://github.com/karinafrank/karinafrank-cluster_analysis_for_median_graduation_time_across_doctorate_programs_at_duke_university/tree/master/Raw%20Data%20Files) were downloaded with data on each individual life science PhD program offered. The data from PDFs was extracted and transformed into [Excel files](https://github.com/karinafrank/karinafrank-cluster_analysis_for_median_graduation_time_across_doctorate_programs_at_duke_university/tree/master/Raw%20Data%20Files) using [Tabula] (https://tabula.technology/). A new [data analysis Excel document](https://github.com/karinafrank/karinafrank-cluster_analysis_for_median_graduation_time_across_doctorate_programs_at_duke_university/blob/master/Clustering%20Data%20Analysis.xlsx) was then created to perform cluster analysis using the following steps:
1. All data regarding median time for degree from separate Excel documents were transfered to one Excel sheet
2. Some data extraction from Tabula was not perfect, so an additional columnn had to be made for AT 2009-11 for each program, and the data was properly separated from its label using the text-to-columns function
3. Since time to graduation data was provided over three cohorts of students, the average and standard deviation of the data was calculated for men and women in each degree program
4. The overall average and standard deviation of time to graduation was calculated across all degree programs
5. The z-score for men and women was calculated using the "standardize" function in Excel, which used the overall average of graduation time and program-specific graduation time for men and women. The code used a "locking" feature when referencing the overall average graduation time, as it was unchanging across degree program, and allowed for changes in input data for program-specific time as the code was extended horizontally. An example of the code used is shown below:
```
=STANDARDIZE(C$3,$BN$3,$BN$4)
```
6. Each degree program was then assigned a number to allow for reference later during the clustering process
7. 3 sets of random clusters were then assigned to allow for a starting point for the Solver program to later optimize.
  * The originally chosen clusters were 2 (Biology), 4 (Cell Biology), and 6 (Computational Biomedical Engineering).
8. The z-score for men and women was computed for these initial clusters, as it would serve as a reference point to check distance against to measure how close other data points were to that cluster.
9. The sum of squares of differences were then calculated between each program's z-score for men and women and each separate cluster program's z-scores for men and women. This calculates how close each program's data is relative to the cluster data, and provides a measure for optimization. An example of the code used is shown below:
```
=SUMXMY2($BQ$4:$BQ$5,B$18:B$19)
```
10. To assign each program to which cluster it belongs (the cluster with the smallest sum of difference of squares), the =MIN function was used to return the value of the smallest difference of squares, and therefore the associated cluster
11. The =MATCH function was then used to return the place value of the previously found minimum difference of squares value. For example, if the fisrt number was found to be the smallest (and associated with the first cluster), then the number 1 was returned. This allows for direct reference to the clusters by number.
12. The sum of all the minimum distance squared values was calculted across all programs, serving as a measure of the overall success of the current clusterings in minimizing distance for all points from their assigned cluster point. 
13. The Solver tool was then used to optimize the cluster sets by setting the objecting to minimize the previously calculated sum of minimum distance squared (see step 12). The program was allowed to change the values of the program IDs (which reference the cluster data to the program data, and allow for different data sets to be switched out). As the program IDs went from 1-21, the Solver tool was provided the constraints that any changes to inputs must be integers, and must be greater than or equal to 1, and less than or equal to 21. The solving method was also specified as evolutionary. 
14. The Solver tool was run, and went through many iterations before timing out and providing its output of the clusters it found to minimize the total difference of squares for all the programs. The final output is shown below.

Clusters|	1|	2|	3
:---:|:---:|:---:|:---:
ID	|12|	6|	7
Name|	Immunology	|Computational BME	|Earth and Ociean Sciences
Z_men	|1.542203733	|-0.126180305	|-3.266667907
Z_women|1.004324571|	-0.126983566|	-2.632023013

15. The outputs then allowed the data to be organized into their assigned clusters based on their minimum distance to each cluster and their cluster match number. A table was created with cluster data grouped together, and a scatter plot was created to represent the data visually

![alt text]()
![alt text](https://github.com/karinafrank/karinafrank-cluster_analysis_for_median_graduation_time_across_doctorate_programs_at_duke_university/blob/master/Cluster%20Graph.JPG)




•	What kind of data was important to use to answer this question, how did you find it, and why did you use this information? Was there some data that you wish you had? If so, how would you change your approach?
•	What metrics did you think were important to understanding a quantitative answer to your original question and why? Did you “translate” any of your data into numbers?
•	Did you base your data analysis on another type of analysis or desired outcome?
•	Use website links to your data sources, for example, if you used data from Baltimore City Open Data, add a link for the reader to learn more.
