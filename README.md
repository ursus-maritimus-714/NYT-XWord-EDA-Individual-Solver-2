
# Exploratory Data Analysis of Individual Solver 2 (IS2) Performance on the New York Times Crossword Puzzle
 
 ## Introduction

### Project Overview
This summary reports on exploratory data analysis (EDA) of an individual solver's (Individual Solver 2; IS2) performance over a large subset of nearly 6 years (Mar. 2018 - Jan. 2024) of the [New York Times (NYT) crossword puzzle](https://www.nytimes.com/crosswords). Included are visual and statistical descriptions of trends in IS2 solve times across this period, IS2 performance relative to the 'Global Median Solver' (GMS; see next section), and the relationship between IS2 performance and a number of variables. These variables included properties of the puzzle grids (e.g., number of answers, number of black squares), properties of clues and answers (e.g., frequency of wordplay in clues, aggregate rarity of answers in a puzzle), environment (e.g., time of day a puzzle was completed), constructor identity, and IS2 puzzle day-of-week-specific past performance prior to a given solve. This EDA led to identification of a set of features that hold promise as useful inputs to a predictive model of IS2 future performance.

This project would not have been possible without access to two key data sources. The first, [XWord Info: New York Times Crossword Answers and Insights](https://www.xwordinfo.com/), was my source for data on the puzzles themselves. This included a number of proprietary metrics pertaining to the grids, answers, clues and constructors. XWord Info has a contract with NYT for access to the raw data underlying these metrics, but I unfortunately do not. Therefore, I will not be able to share raw or processed data that I've acquired from their site (though [Jupyter notebooks](https://jupyter.org/) with all of my Python code for analysis and figure generation can be found [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/tree/main/notebooks)). The second, [XWStats](xwstats.com), was my source for historical solve time data (for both IS2 and the GMS). 

The same analyses reported here for IS2 here were also carried out for my own (IS1) solve data over a comparable sample size and timespan, and are summarized [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1?tab=readme-ov-file#readme).

### The Global Median Solver (GMS)

Many analyses included in this summary compare IS2 performance to that of the GMS over the same set of puzzles. My extensive summary analysis of GMS performance on all puzzled issued over a 6+ year timeframe (2018-2024) can be found [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Global-Median-Solver?tab=readme-ov-file#readme). XWStats (Matt) determines the global median solve time (GMST) for every individual puzzle from a pool of ~1-2K individual solvers of a given puzzle for whom he has (with their consent) acquired their data from NYT. Though Matt adopted the term "global" to describe this solver sample per-puzzle, it likely skews faster than the overall population of solvers. The reasons for this assumption are twofold; only solvers who actually complete a given puzzle are included in its sample, and each sample contains only solvers motivated enough by the prospect of improvement to track their own progress to begin with. 

GMSTs improved over the complete set of puzzles issued between January 1, 2018 and January 13, 2024 (**Figure 1**), with fairly dramatic improvement seen early on for some puzzle days and graded improvement continuing for each puzzle day until the end of the sample period (top panel). The 2-year interval density plots of raw solve time distributions (bottom panels) show that performance on individual puzzle days became more consistent over time (higher peaks with narrower distributions). Because I did not have access to the raw solver data from which the GMSTs were drawn, however, it's not possible to disentangle improvement for individual "early adopters" of Matt's tracking software versus stronger solvers joining the solver pool over time. Note also that GMS performance is tracked in my analyses by puzzle issue date, as I did not have access to GMS puzzle completion dates. It's reasonably safe to assume, however, that the GMS (a different individual solver for most puzzles, presumably) solved in approximately the sequence of puzzle issue. IS2 performance, however, is tracked by puzzle completion data since I *was* able to obtain completion timestamps for their solves with Matt's assistance.  

**Figure 1. GMS Solve Time 10-Puzzle Moving Averages and Distributions by Puzzle Day**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/0c05e987-716c-47a9-bd79-9514479fb1b5)

## Results
### Individual Solver 2 (IS2) Performance Over Time

IS2 solved N = 1,024 puzzles in the sample period: 89 (8.7%) in 2018, 9 in 2019 (.8%), 282 in 2020 (27.5%), 28 (2.7%) in 2021, 79 (7.7%) in 2022, and 537 (52.4%) in 2023/24 (through Jan. 13, 2024). The total solve time for IS1 was 16.6 days (2018: 2.2 days; 2019: .14 days; 2020: 5.1 days; 2021: .25 days; 2022: .97 days; 2023/24: 8.0 days). The total solve time for the GMS over this same set of puzzles was 13.6 days. 

IS2's per-puzzle day 10-puzzle moving averages across the sample period are shown in **Figure 2** (top panel). The first 5 years were characterized by long periods of little solve activity (flat stretches in lines) punctuated by rapid and dramatic improvements across puzzle days during months-long bursts of activity. There was a short-term ("spiked") increase in solve times across puzzles days shortly after significant solving resumed after a long layoff in Q2 2023. Then, from late Q3 2023 through the end of the sample period, IS2 showed dramatic improvement across puzzle days relative to even pre-spike baselines. **Supplementary Figure 1** shows that the solve time in 2023 was *not* likely due to an extended run of unusually difficult puzzles. Improvement over the last ~4 months of the sample period was especially apparent on the more difficult puzzle days (Thu-Sun). Leftward shifts of peaks and reduced bimodality of by-day solve time distributions in the 2023/2024 density plot (**Fig. 2** bottom right) also demonstrate this recent improvement in solve form. 

**Figure 2. 10-Puzzle Solve Time Moving Averages and Distributions by Puzzle Day**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/820dfbae-1053-4eab-ad0c-f55f04e721ac)




**Figure 3** shows IS2's solve time performance trajectory in 2-3 year solve interval violin plots with swarm plot overlays. These representations may be somewhat easier to digest than the line plots in **Fig. 2**, as it removes the visual compressing effect of the long intervals with minimal solve activity. They also have the advantage of giving a clear visual sense of the number of solves per interval. Violin plots show both the range (vertical extent) and distribution characteristics (width as it varies across the y-axis range) for each puzzle day, per solve year. Black lines on the violin plot demarcate solve time quartiles per puzzle day. Swarm plot overlays per puzzle day show individual puzzle raw solve times.**   

**Figure 3. Violin Plots With Swarm Plot Overlay by Puzzle Day**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/f783bca2-b950-4449-aaf5-d27039787bbd)

*<h5>Median[IQR] solve time (m), per puzzle day, per solve interval:*<br>
*2018/19: Sun: 69.3[59.4-82.2], Mon: 10.3[8.7-11.8], Tue: 15.4[11.2-24.5], Wed: 21.5[14.9-34.2], Thu: 43.4[39.6-63.8], Fri: 33.3[30.7-48.5], Sat: 52.0[41.7-55.7]*<br>
*2020-22: Sun: 43.0[36.6-52.4], Mon: 7.1[5.9-8.2], Tue: 10.6[8.7-12.6], Wed: 14.0[11.5-20.0], Thu: 25.0[18.2-31.0], Fri: 26.3[18.4-32.0], Sat: 34.8[28.0-50.4]*<br>
*2023/24: Sun: 32.7[27.1-41.1], Mon: 5.7[4.8-6.5], Tue: 7.4[6.8-8.6],   Wed: 11.9[9.8-14.3], Thu: 19.7[15.8-26.4], Fri: 19.4[15.0-25.0], Sat: 26.4[20.3-36.7]*<br>

###
Because over half of IS2' total solves (n=537) came in 2023-2024, and there was such rapid and dramatic improvement over the latter ~1/3 of that time range, zoom-in and 2-interval partition is depicted below in **Figure 4**. IS2 had n=290 solves in the final 3.5 months of the time range, spread roughly equivalently across puzzle days. The dramatically improved solve performance (the Sat median solve time, for ex. was cut nearly in half) during this period was likely heavily influenced by the large amount of solving in a condensed period of time.    

**Figure 4. IS2 Solve Performance 2023-2024 (Split Interval)**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/e316faf9-29c7-4116-81aa-1d03edca7f91)
*<h5> Note that there were no solves in 2023 before 04/14*<br>

*<h5>Median[IQR] solve time (m), per puzzle day, per solve interval:*<br>
*Apr 2023-Sept 2023: Sun: 41.2[32.6-47.1], Mon: 5.9[5.5-6.7], Tue: 7.7[6.9-8.9], Wed: 13.2[10.6-14.9], Thu: 26.4[18.9-32.1], Fri: 24.2[18.0-32.0], Sat: 38.5[26.7-46.1]*<br>
*Oct 2023-Jan 2024:  Sun: 28.8[23.9-35.4], Mon: 5.4[4.7-6.2], Tue: 7.3[6.6-8.5], Wed: 10.2[8.5-12.4], Thu: 16.9[14.5-20.5], Fri: 18.3[13.0-24.7], Sat: 23.3[17.2-32.5]*<br>



### Individual Solver 2 (IS2) Performance Vs Global Median Solver (GMS) 

The next series of figures directly compare IS2 solve performance to that of the GMS over the same set of puzzles. **Figure 5** shows per-puzzle day scatterplots of raw GMSTs (x-axis) versus IS2 solve times (y-axis), broken down by pre-2023 (lighter dots) and 2023/24 (darker dots) IS2 solve dates. Points falling on the dashed diagonal line represent identical raw solve times for IS2 and GMST on a given puzzle, points above and below this line represent "wins" for the GMS and IS2, respectively. Win %s for IS2 increased dramatically for most puzzle days in 2023/24, including a nearly 2x increase (37.2% to 68.9%) for Tuesday. The lowest IS2 win % for both time intervals was for Saturday, and Monday had the highest and second highest win %s in the pre-2023 and 2023/24 intervals, respectively. The per-day and interval regression lines show exclusively moderate-to-strong positive raw solve time correlations (ranging from .54 to .81) between IS2 and GMS. The downward shifts in all puzzle day regression lines between the older and more recent solve intervals indicates improved performance relative to the GMS. However, a caveat in interpretation here is that IS2 solved many older puzzles in 2023-2024, so the GMS was earlier on "their" own improvement curve when solving the same puzzles. The next figure will remove this issue by examining the IS2-GMS solve time relationship on data normalized to each solver's respective 10-puzzle moving average for a given solve (completion date for IS2 and issue date for GMS). 

**Figure 5. Scatterplots of IS2 vs GMS Solve Performance by Puzzle Day and Solve Interval**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/64fb4d75-122c-40f2-b29b-0d91fc36fd80)

*<h5> Win Percentage for IS2 vs GMS, by IS2 solve interval:*<br>
*pre-2023: Sun: 25.8, Mon: 51.2, Tue: 37.2, Wed: 33.8, Thu: 24.7, Fri: 26.1, Sat: 21.1*<br>
*2023/24:  Sun: 44.6, Mon: 62.3, Tue: 68.9, Wed: 51.6, Thu: 37.8, Fri: 37.3, Sat: 26.2*<br>

*<h5> Mean(stdev) Solve Time Difference (m) for IS2 vs GMS, by IS2 solve interval (negative denotes faster for IS2):*<br>
*pre-2023:   Sun: 9.0(13.4), Mon: .54(2.3), Tue: 1.6(3.4), Wed: 2.9(2.1), Thu: 7.9(11.1), Fri: 7.1(11.7), Sat: 13.2(15.2)*<br>
*2023/24:    Sun: 2.2(8.6), Mon: 0(1.2), Tue: -.48(1.1), Wed: .44(3.2), Thu: 3.4(7.1), Fri: 3.9(8.7), Sat: 8.8(12.9)*<br>

###
Along with comparison of raw solve performance between IS2 and GMS, the degree to which the same puzzles were *relatively* difficult for IS2 and the GMS was addressed. Each IS2 and GMS solve time was taken as a % difference from the solver's respective day-specific 10-puzzle moving average. These 'recent form-normalized' solve times for IS2 and the GMS were then plotted against each other on a per-puzzle day and per-solve interval basis (**Figure 6**). Points falling in the lower left (LL; "relatively easy for both solvers") and upper right (UR; "relatively hard for both solvers") quadrants represent concordance of relative difficulty for a given puzzle. By far the most common outcome across puzzle days for both solve periods was "relatively easy for both solvers" (LL), with the second most common outcome being "relatively hard for both solvers" (UR). One reason for the asymmetry between these two quadrants is that it's relatively rare for the solver (either the GMST or individual solver) to solve a new puzzle more slowly than their 10-puzzle moving average, due to relentless improvement in underlying skill. Nonetheless, there were a substantial number of puzzles in the quadrants other than LL. In fact, UL ("relatively easy for GMS, relatively hard for IS2") was the second most frequent quadrant on multiple puzzle day intervals, including for both Friday time intervals. Starting in the next section, the focus is on analyses isolating the relationship of factors independent of baseline solver aptitude (ie, "why are there points in those three quadrants?".

**Figure 6. IS2 vs GMS Solve Times as Percentage Difference from 10-Puzzle Moving Average by Puzzle Day and Solve Interval**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/edcf174d-749d-42f8-85a4-fc5c7d925094)
*Correlations between IS2 and GMS solve times for a given puzzle day after adjustment for baseline performance were moderately-to-strongly positive*<br>

*IS2-GMS Correlation (Pearson r) of 10-puzzle moving average-adjusted solve difficulty by IS2 solve interval:<br>
*pre-2023: Sun: .74, Mon: .51, Tue: .71, Wed: .67, Thu: .70, Fri: .59, Sat: .74*<br>
*2023/24:  Sun: .63, Mon: .47, Tue: .72, Wed: .56, Thu: .66, Fri: .51, Sat: .50*<br>

*<h5> IS2-GMS Quadrant Percentage by IS2 solve interval: Lower Left(LL)/Upper Right(UR)/Upper Left(UL)/Lower Right(LR)*<br>
*LL: Relatively Easy for Both IS2 & GMS/ UR: Hard for IS2 & GMS/ UL: Easy for GMS-Hard for IS2/ LR: Easy for IS2-Hard for GMS*<br> 
*pre-2023: Sun: 53.1/18.8/18.8/9.4, Mon: 62.0/19.0/15.2/3.8, Tue: 52.4/17.1/23.2/7.3, Wed: 50.6/16.0/18.5/14.8, Thu: 51.4/25.7/13.5/9.5, Fri: 54.5/19.7/22.7/3.0,<br> Sat: 64.8/18.5/11.1/5.6*<br>
*2023/24:  Sun: 48.6/26.4/13.9/11.1, Mon: 52.5/15.3/23.7/8.5, Tue: 55.7/23.0/19.7/1.6, Wed: 45.9/26.2/14.8/13.1, Thu: 50.0/25.7/17.6/6.8, Fri: 50.0/20.0/25.0/5.0,<br> Sat: 42.2/28.9/16.9/12.0*<br>







# Supplementary Figures

**<h4>Supplementary Figure 1. IS2 10-Puzzle Solve Time Moving Averages, Adjusted by GMS Performance by Puzzle Day** 

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/5e98e0de-2304-48eb-9ad1-60d81fb251ca)
*<h5>For each puzzle completed by IS2, the percentage difference for the raw solve time from the global median solve time (GMST) was computed. The 10-puzzle moving average of this difference was then plotted, per puzzle day, by completion date. The volatility present in the raw solve times (see **Fig. 2**), particularly that around late Q1 2023 (a reminder that these moving averages are lagging indicators) was still mostly present in these adjusted data plots, indicating that this volatility was due to factors other than by-chance runs of greater or lesser difficulty per-puzzle day.*

