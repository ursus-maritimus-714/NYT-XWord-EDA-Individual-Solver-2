
# Exploratory Data Analysis of Individual Solver 2 (IS2) Performance on the New York Times Crossword Puzzle
 
 ## Introduction

### Project Overview
This summary reports on exploratory data analysis (EDA) of an individual solver's (Individual Solver 2; IS2) performance over a large subset of nearly 6 years (Mar. 2018 - Jan. 2024) of the [New York Times (NYT) crossword puzzle](https://www.nytimes.com/crosswords). Included are visual and statistical descriptions of trends in IS2 solve times across this period, IS2 performance relative to the 'Global Median Solver' (GMS; see next section), and the relationship between IS2 performance and a number of variables. These variables included properties of the puzzle grids (e.g., number of answers, number of black squares), properties of clues and answers (e.g., frequency of wordplay in clues, aggregate rarity of answers in a puzzle), environment (e.g., time of day a puzzle was completed), constructor identity, and IS2 puzzle day-of-week-specific past performance prior to a given solve. This EDA led to identification of a set of features that hold promise as useful inputs to a predictive model of IS2 future performance.

This project would not have been possible without access to two key data sources. The first, [XWord Info: New York Times Crossword Answers and Insights](https://www.xwordinfo.com/), was my source for data on the puzzles themselves. This included a number of proprietary metrics pertaining to the grids, answers, clues and constructors. XWord Info has a contract with NYT for access to the raw data underlying these metrics, but I unfortunately do not. Therefore, I will not be able to share raw or processed data that I've acquired from their site (though [Jupyter notebooks](https://jupyter.org/) with all of my Python code for analysis and figure generation can be found [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/tree/main/notebooks)). The second, [XWStats](xwstats.com), was my source for historical solve time data (for both IS2 and the GMS). 

The same analyses reported here for IS2 here were also carried out for my own (IS1) solve data over a comparable sample size and timespan, and are summarized [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1?tab=readme-ov-file#readme).

### The Global Median Solver (GMS)

Many analyses included in this summary compare IS2 performance to that of the GMS over the same set of puzzles. My extensive summary analysis of GMS performance on all puzzled issued over a 6+ year timeframe (2018-2024) can be found [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Global-Median-Solver?tab=readme-ov-file#readme). XWStats (Matt) determines the global median solve time (GMST) for every individual puzzle from a pool of ~1-2K individual solvers of a given puzzle for whom he has (with their consent) acquired their data from NYT. Though Matt adopted the term "global" to describe this solver sample per-puzzle, it likely skews faster than the overall population of solvers. The reasons for this assumption are twofold; only solvers who actually complete a given puzzle are included in its sample, and each sample contains only solvers motivated enough by the prospect of improvement to track their own progress to begin with. 

GMSTs improved over the complete set of puzzles issued between January 1, 2018 and January 13, 2024 (**Figure 1**), with fairly dramatic improvement seen early on for some puzzle days and graded improvement continuing for each puzzle day until the end of the sample period (top panel). The 2-year interval density plots of raw solve time distributions (bottom panels) show that performance on individual puzzle days became more consistent over time (higher peaks with narrower distributions). Because I did not have access to the raw solver data from which the GMSTs were drawn, however, it's not possible to disentangle improvement for individual "early adopters" of Matt's tracking software versus stronger solvers joining the solver pool over time. Note also that GMS performance is tracked in my analyses by puzzle issue date, as I did not have access to GMS puzzle completion dates. It's reasonably safe to assume, however, that the GMS (a different individual solver for most puzzles, presumably) solved in approximately the sequence of puzzle issue. IS2 performance, however, is tracked by puzzle completion data since I *was* able to obtain completion timestamps for their solves with Matt's assistance.  

**Figure 1. GMS Solve Time 10-Puzzle Moving Averages and Distributions by Puzzle Day (2-Year Issue Date Intervals)**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/0c05e987-716c-47a9-bd79-9514479fb1b5)

## Results
### Individual Solver 2 (IS2) Performance Over Time

IS2 solved N = 1,024 puzzles in the sample period: 89 (8.7%) in 2018, 9 in 2019 (.8%), 282 in 2020 (27.5%), 28 (2.7%) in 2021, 79 (7.7%) in 2022, and 499 (48.8%) in 2023/24 (through Jan. 13, 2024). The total solve time for IS1 was 16.6 days (2018: 2.2 days; 2019: .14 days; 2020: 5.1 days; 2021: .25 days; 2022: .97 days; 2023/24: 8.0 days). The total solve time for the GMS over this same set of puzzles was 13.6 days. 

IS2's per-puzzle day 10-puzzle moving averages across the sample period are shown in **Figure 2** (top panel). The first 5 years were characterized by long periods of little solve activity (flat stretches in lines) punctuated by rapid and dramatic improvements across puzzle days during months-long bursts of activity. Rapid improvements across puzzle days were then seen again across puzzle days when solving resumed in early 2023, followed by an abrupt increase in solve times (potentially related to transient health issues; **Supplementary Figure 1** shows that solve time volatility in 2023 was *not* likely due to coincidental cyclical changes in the difficulty of puzzles). From the middle of 2023 until the end of the sample period, IS2 once again showed dramatic improvement even relative to pre-transient upward spike baselines. Improvement over the last ~8 months of the sample period was especially apparent on the more difficult puzzle days (Thu-Sun). Leftward shifts of peaks and reduced bimodality of by-day solve time distributions in the 2023/2024 density plot (**Fig. 2** bottom right) also demonstrate this recent improvement in solve form. 

**Figure 2. 10-Puzzle Solve Time Moving Averages and Distributions by Puzzle Day (2- or 3-Year Solve Date Intervals)**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/b0bfe922-8742-40a1-80f6-d132bd105614)


**Figure 3** shows IS2's complex solve time performance trajectory in 2-3 year interval violin plots with swarm plot overlays. These representations may be somewhat easier to digest than the line plots in **Fig. 2**, as it removes the visual compressing effect of the long intervals with minimal solve activity. They also have the advantage of giving a clear visual sense of the number of solves per interval. Violin plots show both the range (vertical extent) and distribution characteristics (width as it varies across the y-axis range) for each puzzle day, per solve year. Black lines on the violin plot demarcate solve time quartiles per puzzle day. Swarm plot overlays per puzzle day show individual puzzle raw solve times.**   

**Figure 3. Violin Plots With Swarm Plot Overlay by Puzzle Day (2- or 3-Year Solve Date Intervals)**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/181372d2-8926-46cb-a064-1da66e56bcdc)




# Supplementary Figures

**<h4>Supplementary Figure 1. IS2 10-Puzzle Solve Time Moving Averages, Adjusted by GMS Performance by Puzzle Day** 

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/5e98e0de-2304-48eb-9ad1-60d81fb251ca)
*<h5>For each puzzle completed by IS2, the percentage difference for the raw solve time from the global median solve time (GMST) was computed. The 10-puzzle moving average of this difference was then plotted, per puzzle day, by completion date. The volatility present in the raw solve times (see **Fig. 2**), particularly that around late Q1 2023 (a reminder that these moving averages are lagging indicators) was still mostly present in these adjusted data plots, indicating that this volatility was due to factors other than by-chance runs of greater or lesser difficulty per-puzzle day.*

