
# Exploratory Data Analysis of Individual Solver 2 (IS2) Performance on the New York Times Crossword Puzzle

## Introduction

### Project Overview
This summary reports on exploratory data analysis (EDA) of an individual solver's (Individual Solver 2; IS2) performance over a large subset of 6 years (Mar. 2018 - Mar. 2024) of the [New York Times (NYT) crossword puzzle](https://www.nytimes.com/crosswords). Included are visual and statistical descriptions of trends in IS2 solve times across this period, performance relative to the 'Global Median Solver' (GMS; see next section), and the relationship between IS2 performance and a number of variables. These variables included properties of the puzzle grids (e.g., number of answers, number of black squares), clues and answers (e.g., frequency of wordplay in clues, aggregate rarity of answers in a puzzle), environment (e.g., time of day a puzzle was completed), constructor identity, and puzzle day-specific recent past performance prior to a given solve. This EDA led to identification of a set of features that were used as inputs to a [predictive model of IS2 future performance](https://github.com/ursus-maritimus-714/NYT-XWord_Modeling-Individual-Solver-2/blob/main/README.md).

Without access to two specific data sources this project would not have been possible. The first, [XWord Info: New York Times Crossword Answers and Insights](https://www.xwordinfo.com/), was my source for data on the puzzles themselves. This included a number of proprietary metrics pertaining to the grids, answers, clues and constructors. XWord Info has a contract with NYT for access to the raw data underlying these metrics, but I unfortunately do not. Therefore, I will not be able to share raw or processed data that I've acquired from their site. Nonetheless, [Jupyter notebooks](https://jupyter.org/) with all of my Python code for analysis and figure generation can be found [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/tree/main/notebooks). The second, [XWStats](https://xwstats.com/), was my source for historical solve time data for both IS2 and the GMS.

Similar analyses to those reported here for IS2 were performed on another individual's (IS1) data over a comparable sample size and timespan, and are summarized [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1?tab=readme-ov-file#readme). In addition, the results of predictive modeling for IS1 are [here](https://github.com/ursus-maritimus-714/NYT-XWord-Modeling-Individual-Solver-1/blob/main/README.md).

### The Global Median Solver (GMS)

Many analyses included in this summary compare IS2 performance to that of the GMS over the set of all IS2 solves. My extensive summary analysis of GMS performance over a 6+ year timeframe (2018-2024) can be found [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Global-Median-Solver?tab=readme-ov-file#readme). Additionally, a summary of predictive modeling of GMS solve performance can now be found [here](https://github.com/ursus-maritimus-714/NYT-XWord-Modeling-Global-Median-Solver/blob/main/README.md). XWStats (Matt) determines the Global Median Solve Time (GMST) for every individual puzzle from a pool of ~1-2K individual solvers from whom he has (with their consent) acquired personal solve data. Though Matt adopted the term "global" to describe this solver sample per puzzle, it likely skews faster than the overall population of solvers. The reasons for this assumption are twofold; only solvers who actually complete a given puzzle are included in its sample, and each sample contains only solvers motivated enough by the prospect of improvement to track their own progress to begin with. 

GMSTs improved on each puzzle day over the complete set of puzzles (N=2,252) issued between January 1, 2018 and March 1, 2024 (**Figure 1**). This improvement was fairly dramatic in the first few years for some puzzle days (most prominently for Sun), and graded improvement continued for each puzzle day until the end of the sample period (top panel). The 2-year interval density plots of raw solve time distributions (bottom panels) show that performance on individual puzzle days became more consistent over time (higher peaks with narrower distributions). Because I did not have access to the raw solver data from which the GMSTs were drawn, however, it was not possible to delineate how much of the improvement was due to individual "early adopters" of Matt's tracking software getting faster and more consistent over time versus due to stronger solvers joining the solver pool over time. Note also that GMS performance was tracked in my analyses by puzzle issue date, as I did not have access to GMS puzzle completion dates. It's reasonably safe to assume, however, that the GMS (a different individual solver for most puzzles, presumably) solved in approximately the sequence of puzzle issue. IS2 performance, in contrast, was tracked by puzzle completion data since I *was* able to obtain completion timestamps for this solver with Matt's assistance.  

**<h4>Figure 1. GMS Solve Time Overview by Puzzle Day: 10-Puzzle Moving Averages and Distributions of Raw Values**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/83521174-66a8-4740-a2c7-d8769fd0b974)
*<h5>GMS Final (as of Mar. 1, 2024) 10-puzzle moving average of solve time (m), per puzzle day:*<br>
*Sun: 28.9, Mon: 5.6, Tue: 7.7, Wed: 11.3, Thu: 17.4, Fri: 17.6, Sat: 19.2*<br>

## Results
### Individual Solver 2 (IS2) Performance Over Time

IS2 solved N = 1,230 puzzles in the sample period: 89 (7.2%) in 2018, 9 in 2019 (.7%), 282 in 2020 (22.9%), 28 (2.3%) in 2021, 79 (6.4%) in 2022, 499 (40.6%) in 2023 and 244 (19.8%) in 2024 (through Mar. 2). The total solve time for IS2 was 18.8 days (2018: 2.2; 2019: .14; 2020: 5.1; 2021: .25; 2022: .97; 2023: 7.6; 2024: 2.6). The total solve time for the GMS over this same set of puzzles was 16.2 days. 

IS2's per puzzle day 10-puzzle moving averages across the sample period are shown in **Figure 2** (top panel). The first 5 years were characterized by long periods of little solve activity (flat stretches in lines) punctuated by rapid and dramatic improvements across puzzle days during months-long bursts of activity. There was a short-term, spiked increase in solve times across puzzles days when solving resumed in Q2 2023 after a long layoff. Then, from late Q3 2023 through the end of the sample period, IS2 showed dramatic improvement across puzzle days relative to even pre-spike baselines. **Supplementary Figure 1** shows that the volatility of IS2's per puzzle day solve times in 2023 was *not* likely due to chance stretches of puzzles with higher or lower than usual median difficulty (as determined by GMS performance on the same puzzle set). Improvement over the last ~5 months of the sample period was especially apparent on the more difficult puzzle days (Thu-Sun). The leftward shift in peaks for the by day solve time distributions in the 2023/2024 density plot (**Fig. 2**, bottom right) clearly demonstrates this recent improvement in solve form. Additionally, overall distribution widths narrowed considerably across solve intervals for early week (Mon-Wed) puzzle days. This indicates increased consistency of solve performance over time for IS2.    

**<h4>Figure 2. IS2 Solve Time Overview by Puzzle Day: 10-Puzzle Moving Averages and Distributions of Raw Values**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/168d3684-859f-4c61-b886-05d709bc8420)
*<h5>IS2 Final (as of Mar. 2, 2024) 10-puzzle moving average of solve time (m), per puzzle day:*<br>
*Sun: 24.4, Mon: 5.7, Tue: 6.6, Wed: 10.1, Thu: 15.4, Fri: 15.6, Sat: 24.0*<br>

###

**Figure 3** shows IS2's solve time performance trajectory in violin plots with swarm plot overlays, broken out by solve interval (the first solve interval [2018/19] is reported separately as **Supplementary Figure 2**). These representations may be somewhat easier to digest than the line plots in **Fig. 2**, as they remove the compressing effect of the long intervals with minimal solve activity. They also have the advantage of providing a clear visual sense of the number of solves and distribution shapes, per interval. Violin plots show both the range (vertical extent) and distribution characteristics (width as it varies across the y-axis range) for each puzzle day, per solve interval. Black lines on the violin plots demarcate solve time quartiles per puzzle day. Swarm plot overlays per puzzle day show individual puzzle raw solve times. The narrow geometries of the later week violin plots relative to the earlier week ones correspond to greater relative performance variability on those solve days. This phenomenon will be discussed in the final section of the summary in the context of correlation between past and future performance and prospects for predictive modeling.  

**<h4>Figure 3. IS2 Solve Time Overview by Puzzle Day: Violin Plots With Swarm Plot Overlay**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/eea4cf7d-c813-4a6c-9b5d-7c3a8eac1fe2)
*<h5>Median[IQR] solve time (m), per puzzle day, per solve interval:*<br>
*2020-22: Sun: 43.0[36.6-52.4], Mon: 7.1[5.9-8.2], Tue: 10.6[8.7-12.6], Wed: 14.0[11.5-20.0], Thu: 25.0[18.2-31.0], Fri: 26.3[18.4-32.0], Sat: 34.8[28.0-50.4]*<br>
*2023   : Sun: 33.0[27.7-42.9], Mon: 5.7[4.9-6.5], Tue: 7.5[6.8-8.7],   Wed: 11.1[9.7-14.3], Thu: 20.2[15.9-28.8], Fri: 22.3[14.8-29.7], Sat: 30.9[23.1-42.2]*<br>
*2024   : Sun: 23.9[20.9-28.2], Mon: 4.9[4.2-5.9], Tue: 6.9[6.4-8.0],   Wed: 9.9[7.6-11.8], Thu: 15.3[13.3-20.6], Fri: 15.6[11.7-17.8], Sat: 19.6[16.0-24.0]*<br>

###
Because >60% of IS2' total solves (n=743) took place in 2023 or 2024, and there was such rapid and dramatic improvement over the latter ~1/3 of that time range, zoom-in and 2-interval partition of this time range is depicted below in **Figure 4**. IS2 completed n= 496 (66.8%) of these solves in the final 5 months of this time range, spread roughly equivalently across puzzle days. The dramatically improved solve performance (Sat median solve time, for ex., dropped from 38.5 to 22 minutes) during this period was likely enhanced by the high volume of solving in a condensed time frame.    

**<h4>Figure 4. IS2 Solve Performance in 2023-2024**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/2013a18d-61e9-4188-ba8f-11ec72009956)
*<h5>Median[IQR] solve time (m), per puzzle day, per solve interval:*<br>
*Apr 2023-Sept 2023: Sun: 41.2[32.6-47.1], Mon: 5.9[5.5-6.7], Tue: 7.7[6.9-8.9], Wed: 13.2[10.6-14.9], Thu: 26.4[18.9-32.1], Fri: 24.2[18.0-32.0], Sat: 38.5[26.7-46.1]*<br>
*Oct 2023-Mar 2024:  Sun: 26.9[22.9-32.2], Mon: 5.4[4.5-6.2], Tue: 7.0[6.6-8.2], Wed: 10.1[8.1-12.4], Thu: 16.5[13.4-20.8], Fri: 16.2[12.6-21.0], Sat: 22.0[16.8-26.2]*<br>


### Individual Solver 2 (IS2) Performance Vs Global Median Solver (GMS) 

The next series of figures directly compare IS2 solve performance to that of the GMS over the same puzzle set. For these analyses, IS2 solves were broken into 2 solve intervals: pre-2023 (n=487; 39.7% of total solves); 2023/24: n=740; 60.3%). Per puzzle day, pre-2023 solves are represented by lighter-colored points and regression lines and 2023/24 solves by darker-colored ones. 

**Figure 5** shows per puzzle day scatterplots of raw GMSTs (x-axis) versus raw IS2 (y-axis) solve times. Points falling on the dashed diagonal line represent identical raw solve times for the GMS and IS2 on a given puzzle. Points above and below this line represent "wins" for the GMS and IS2, respectively. IS2 win % across all puzzle days improved greatly, nearly doubling between the pre-2023 (28.7%) and 2023/24 (57.1%) solve intervals. Win %s for IS2 also increased dramatically for most puzzle days in 2023/24, including >2x increases for 6/7 puzzle days. This included the most difficult puzzles days; Friday (22.2% to 53.2%) and Saturday (13.7% to 40.3%). The lowest IS2 win % for both time intervals was for Saturday. Monday yielded the highest win rate for IS2 in the pre-2023 interval (48.1%), but Tue had the highest IS2 win rate for the 2023/24 interval by a substantial margin (75%, as compared to 67% for Mon). The mean magnitude of performance advantage for the GMS over IS2 also decreased greatly in the more recent solve interval for all puzzle days together (6.1 to 1 minutes), as well as for all individual puzzle days (with IS2 gaining the advantage by this measure on Sun and Mon-Wed of the 15x15 puzzle days). 

Per puzzle day regression lines show that there was a high degree of correlation (Pearson correlation coefficient; r) for raw solve times between the GMS and IS2 (2023/24 all puzzles: .85; individual puzzle day range: .54-.78). The next figure addresses this correlation in a way that is normalized for recent (prior to a give solve) baseline performance, per solver. This is particularly useful for IS2, since this solver completed many older puzzles in 2023-2024. Thus, the GMS was earlier on "their" own improvement curve when solving the same puzzles.   

**<h4>Figure 5. IS2 vs GMS: Comparison of Raw Solve Performance by Puzzle Day and Solve Interval**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/a63c91de-cf25-4151-817e-5988b9891bd0)
*<h5> Win % for IS2 vs GMS, by IS2 solve interval:*<br>
*pre-2023: All: 28.7, Sun: 24.2, Mon: 48.1, Tue: 34.6, Wed: 29.1, Thu: 20.8, Fri: 22.2, Sat: 13.7*<br>
*2023/24:  All: 57.1, Sun: 57.7, Mon: 67.0, Tue: 75.0, Wed: 62.1, Thu: 51.7, Fri: 53.2, Sat: 40.3*<br>

*<h5> Mean(stdev) Solve Time Difference (m) for IS2 vs GMS, by IS2 solve interval (negative denotes faster for IS2):*<br>
*pre-2023: All: 6.1(10.5), Sun: 9.6(13.6), Mon: .64(2.3), Tue: 1.8(3.4), Wed: 3.4(6.1), Thu: 8.7(11.1), Fri: 7.9(11.8), Sat: 15.3(14.8)*<br>
*2023/24:  All: 1.0(7.9), Sun: -.49(8.8), Mon: -.26(1.2), Tue: -.91(1.3), Wed: -.51(3.3), Thu: 1.1(7.0), Fri: 1.4(8.3), Sat: 5.6(12.7)*<br>

###
Along with comparison of raw solve performance between IS2 and GMS, the degree to which the same puzzles were *relatively* difficult for the two solvers was addressed. For IS2, each raw solve time was taken as a % difference from a *non*-weighted average of the *previous* 10 puzzles solved on the same puzzle day (Recent Performance Baseline; RPB). For the GMS, this RPB metric was derived using a decay-time weighted average of the previous 40 puzzle day-specific puzzles solved by the GMS. The reason for this difference is that the early stages of predictive modeling revealed these different respective RPB strategies to yield the best predictions, per solver. See Methods sections of [summary of predictive modeling for GMS](https://github.com/ursus-maritimus-714/NYT-XWord-Modeling-Global-Median-Solver/blob/main/README.md) and [IS2](https://github.com/ursus-maritimus-714/NYT-XWord_Modeling-Individual-Solver-2/blob/main/README.md) for details and links to code of the experiments leading to this dichotomy.   

RPB-adjusted solve times for the GMS (x-axis) and IS2 (y-axis) were then plotted against each other on a per puzzle day and per solve period basis (**Figure 6**). Points falling in the lower left ("relatively easy for both solvers") and upper right ("relatively hard for both solvers") quadrants represent concordance of relative difficulty for a given puzzle. The most common outcome across puzzle days for both solve periods was "relatively easy for both solvers" (pre-2023: 50.8%; 2023/24: 47.6%), and the second most common was "relatively hard for both solvers" (pre-2023: 19.6%; 2023/24: 24.4%).  

It's no surprise that "easy" concordance was more common than "hard" concordance, since solvers constantly improved/outperformed their RPB on a puzzle-to-puzzle basis. A substantial minority (~30%) of puzzles, however, were either relatively easy for IS2 and relatively hard for GMS or vice versa (lower right and upper left quadrants, respectively). Of the two discordant quadrants, "relatively easy for IS2 and relatively hard for the GMS" was more common in both solve intervals across puzzle days (17.1% vs 12.5% and 16.6% vs 11.2%, respectively). The considerable % of puzzles falling into discordant quadrants suggests that environmental and puzzle-specific variables may affect different solvers in different ways. Starting in the next section, the focus will be on summarizing the effects of some of these variables on IS2 (and GMS) performance.    

**<h4>Figure 6. IS2 vs GMS: Comparison of Baseline-Adjusted Solve Performance by Puzzle Day and Solve Interval**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/0846e5b6-189a-4358-b22a-ece359e57cd8)
*<h5> IS2-GMS Quadrant % by IS2 solve period:*<br>
*LL: Relatively Easy for Both IS2 & GMS/ UR: Hard for IS2 & GMS/ UL: Easy for GMS-Hard for IS2/ LR: Easy for IS2-Hard for GMS*<br> 
*pre-2023: All: 50.8/19.6/17.1/12.5, Sun: 55.7/18.0/16.4/9.8, Mon: 51.3/16.7/20.5/11.5, Tue: 46.3/21.3/18.8/13.8, Wed: 46.2/16.7/17.9/19.2, Thu: 53.5/23.9/14.1/8.5,<br> Fri: 50.0/17.7/22.6/9.7, Sat: 56.0/24.0/6.0/14.0*<br>
*2023/24:  All: 47.8/24.5/16.6/11.2, Sun: 51.0/23.1/15.4/10.6, Mon: 49.5/16.5/22.0/12.1, Tue: 52.2/25.0/13.0/9.8, Wed: 45.3/29.5/9.5/15.8, Thu: 42.4/29.7/13.6/14.4,<br> Fri: 48.4/18.5/26.6/6.5, Sat: 47.0/28.6/14.3/10.1*<br>

### IS2 Performance by Puzzle Constructor(s)

A high proportion of puzzles solved by IS2 (72.1%) were authored by either repeat individual constructors or repeat specific constructor teams (both referred to as "constructor" from here forward). This afforded the opportunity to evaluate which constructors IS2 tended, in a relative sense, to struggle against or do well against. Per constructor, the mean of % difference from puzzle day-specific recent performance baseline (RPB; see text section pertaining to **Fig. 6**) was computed. This measure allowed assessment of constructor difficulty adjusted for solver form at the time of a given solve and constructor past puzzle day heterogeneity. **Figure 7** shows heatmapping of IS2 performance using this normalized measure, along with GMS performance on the same set of puzzles, against the n=87 constructor(s) contributing >=4 puzzles over the sample period. While only 15.1% of constructor(s) contributed this many puzzles, this group contributed 45% of all puzzles solved by IS2.

Warmer colors (-%) in **Fig. 7** indicate that on average the solver was relatively fast against a given constructor; cooler colors (+%) indicate slower solves. Mean difference from RPB for IS2 solve time against different constructors ranged from -58.9% for "easiest constructor" (Brian Thomas) to +39.3% for "hardest constructor" (Kyle Dolan). The range for the GMS was considerably smaller, from -42.1% for "easiest constructor" (Erik Agard and Andy Kravis) to +15.2% for "hardest constructor" (Byron Walden). "Hot" or "cold" constructors for IS2 tended to be relatively fast or slow, respectively, for the GMS. However, there was clearly a substantial degree of discordance in terms of specific order and some constructors stood out as being either relatively "hot" for IS2 but relatively "cold" for the GMS (e.g., Adrian Johnson, Drew Schmenner, Peter Collins) or vice versa (e.g., Rafael Musa, Natan Last, Ruth Bloomfield Margolin, Will Nediger). 


**<h4>Figure 7. Heatmapping of IS2 and GMS Performance Against Individual Constructors**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/04f6bb2f-a686-4ec1-8509-9ee2b2bfbeea)
*<h5>Constructor rankings are sorted by normalized IS2 relative solve speed. GMS values over the same set of puzzles are included for comparison.*<br>
###
The next correlational analysis was aimed at assessing the potential predictive value of IS2's baseline-adjusted past performance against specific constructors on their future performance against the same constructor. **Figure 8** shows this correlation between IS2 past performance (as mean % difference from RPB) against a given constructor (x-axis) and performance on the next solved individual puzzle by that constructor (y-axis). This analysis was restricted to only the n=289 puzzles by the constructors included in **Fig. 7** that were solved *after* >=3 previous puzzles by the same constructor (based on puzzle completion date for IS2, but issue date for GMS). There was a weak-to-moderate positive correlation for IS2 (r=.23), and a stronger one for GMS (r=.3). This weaker correlation for the individual solver relative to the GMS was also seen for IS1 (see link to analysis in Introduction). This disparity may have been due to the fact that performance for a single solver is inherently subject to more puzzle-to-puzzle variability than that of an "aggregate solver". Regardless, the evident positive correlations for all 3 solvers at relatively low puzzle n's provides optimism that including past performance vs constructor will have predictive value in the modeling phase.     

**<h4>Figure 8. IS2 and GMS: Past Performance Against Individual Constructors as "Prediction" of Next Puzzle Performance Against the Same Constructor**  

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/26d65541-19c2-4c4e-8d8e-825218a9439f)
<h5>Pearson correlation coefficient (r): IS2: .23, GMS: .3

### IS2 Performance by Completion Time of Day

Many external variables are likely to have an impact on individual solver performance, for the large majority of which data collection would be very difficult. Examples include data relevant to how tired, stressed, influenced by caffeine and other substances, or distracted by other sensory stimuli the solver was while working on a given puzzle. The hardware technology used to solve a given puzzle (e.g., phone vs tablet vs computer) will also likely influence solve times in idiosyncratic ways. One external variable that we *are* fortunate to have data on (thanks, once again, to Matt at XWStats) is time of day at puzzle completion. **Figure 9** shows IS2's solve performance by hour of day, overall (black) and by puzzle day (by color). To control for day-specific puzzle difficulty, solve times are expressed as % difference from puzzle day-specific recent performance baseline (RPB). 

The majority of IS2 solves occurred in the evening (65.6% after 6 PM and 35% after 9 PM). One interesting trend was that very few solves between 12-8 AM (2/81; 2.5%) were "very fast" (>=50% faster than day-specific RPB). In contrast, 64/564 (11.5%) solves between 8-11 PM qualified as "very fast". So while there was no striking overall relationship between solve time and hour of completion, IS2's top performances were much more likely (by >4x) to come in the evening than late at night or in the early morning. Nonetheless, interpretation of this result is still difficult because puzzle *start* times were not available. Thus, it can't be distinguished with the available data whether IS2 was a better performer at night or simply finished easier puzzles before bedtime and left harder ones for morning completion. Another caveat is that all solve times were recorded with respect to the US Eastern Time Zone, and there is no indication for if/when individual puzzles were completed in other time zones.    

**<h4>Figure 9. IS2 Recent Performance Baseline-Adjusted Solve Times by Hour of Completion**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/9c65e04d-e0f4-4cfa-ba60-46f54e627498)
*<h5>Times are all US Eastern Time Zone, adjusted for Daylight Savings Time as necessary.*

### Correlations of IS2 Performance on Individual Puzzles to Puzzle-Specific Features and Recent Past Performance

Numerous potentially interesting features pertaining to puzzle grids, clues, and answers were obtained from XWord Info across the sample period. Features showing strong correlation to IS2 solve performance become promising candidates as input features for predictive modeling, in current forms and/or when combined in novel ways with other existing features. **Figure 10** shows correlation heatmapping separately for 15x15 puzzles (Mon-Sat) and 21x21 puzzles (Sun) for a subset of all measured features with distributions amenable to linear regression and correlation analysis (see **Supplementary Figure 3** for individual 15x15 puzzle day matrices). The Pearson correlation coefficient (r) captures linear correlation strength between a given feature and raw solve times (top row and leftmost column of correlation matrix; red indicates a strong positive correlation and green a strong negative correlation). The rightmost column/bottom row per matrix shows the correlation between IS2 raw solve times for individual puzzles and puzzle day-specific recent performance baseline (RPB). For both 15x15 puzzles and 21x21 puzzles, this (positive) correlation was stronger than any other measured feature correlation to IS2 raw solve times. This finding generates a prediction that recent (relative to a puzzle date to be predicted) solver form per puzzle day will be more predictive of performance on a novel puzzle than will be any individual grid, clue or answer feature. 

As can also be seen in the **Fig. 10** correlation matrices, a number of grid, clue and answer-related features correlated strongly with each other. For example, 'Average Answer Length' and 'Freshness Factor' showed a strong negative correlation. This relationship makes intuitive sense because 'Freshness Factor' is a measure of aggregate answer rarity for a given puzzle, and longer answers have a higher likelihood of being uncommon than shorter ones. Additionally, numerous features not selected for this analysis might still be useful in predictive modeling but either had non-continuous distributions (e.g., 0 or 1 for puzzles with normal vs non-standard symmetry) or pertain to a feature that is largely specific to only one or several puzzle days (e.g. Rebuses, Circles, Shaded Squares; see **Supplementary Figures 4-6**). 

One additional note on data inclusion time range: 2018/19 solves (n=98) have been removed for this analysis due to the relatively large degree of volatility in raw solve times seen during that initial interval of IS2's digital solving (see **Fig. 2 and Supp. Figs. 1-2**). Also see discussion in the next section about the tradeoff between being able to identify patterns in the relationships between features and solve times across puzzle days vs accounting for the constantly shifting baseline in performance by normalizing solve times to recent performance baseline (RPB). 

**<h4>Figure 10. Correlation Heatmapping of IS2 Raw Solve Times vs Grid, Clue, Answer and Past Performance Features**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/9a18ca4d-8006-4f9e-94a9-22867841f12b)
*<h5>Correlation heatmaps derived from N=979 15x15 (left panel) and N=153 21x21 (right panel) puzzles solved by IS2 from 2020-2024.*

###
**Figure 11** through **Figure 22** are companion figures to the correlation heatmapping shown in **Fig. 10**. These figures show, across all 15x15 puzzle days (black) and by-puzzle-day (colors), scatterplots of select features of interest vs IS2 raw solve times at the level of individual puzzles. A feature distribution density plot (FDP) shows puzzle day-specific trends in the distribution of each plotted feature. 

Per feature, raw IS2 solve times are plotted on the y-axis of the **all 15x15 puzzle days plot** and the correlation (Pearson r) between raw IS2 solve times and the feature across all 15x15 puzzles is reported. This allowed trends spanning across the full set of 15x15 puzzles to be visualized and quantified. However, for the **puzzle day plots**, IS2 solve times on the y-axis were normalized as % difference from puzzle day-specific recent performance (RPB). This normalization was performed to aid in teasing out potentially subtle correlations between features and solve times on the individual day level that might otherwise have been lost in the noise of the ever-shifting performance baseline. Normalizing the all 15x15 data to remove baseline volatility removes cross-puzzle day trends, trends that we very much would like to see in the evaluation of features for potential inclusion in a predictive model that is agnostic to puzzle day. Hence, the "best of both worlds" approach I've taken here.     

Though most features had at least moderate strength correlations with IS2 solve times across all 15x15 puzzles, at the by puzzle day level these correlations were typically stronger for the more difficult puzzle days (Sat, in particular). Correlations robust enough to show through within a given puzzle day, where many variables related to puzzle difficulty presumably had similar properties across puzzles, are likely to have a meaningful impact on solve times. As is evident across the scatterplot figures below, several factors make it more likely for later week puzzle days (e.g., Sat) to show within-day correlations that may also be associated with predictive value. For one, there may be threshold values per feature below/above which that feature's impact was not significant in comparison with the contribution of solver aptitude (see discussion above about **Fig. 10**, and also see **Fig. 22**). Because late-week puzzle days almost uniformly had considerably wider ranges of feature values than earlier week puzzle days (compare per day widths in the FDPs or x-axis extents in the scatterplots), effects apparent on those late week days may have been severely clipped by limited ranges on the early week days. Secondly, early week puzzles may also simply not have been difficult enough overall for given features (especially grid features, as a clue is only as difficult as the answer content that it houses) to have had discernable impacts on solve times.
    
Each figure caption for **Figs. 11-22** compares the correlation strength for a given feature for IS2 with that for the global median solver (GMS) over the same set of puzzles. While GMS correlations were uniformly directionally the same as for IS2, they were also uniformly *stronger* than those for IS2. This relative strength was likely related to the more variable per day baseline solve performance of IS2 relative to the GMS (**see Figs. 1, 2 and 4**), which in turn relates to one being a single human subject to puzzle-to-puzzle variability in many aspects and the other being a "mathematical entity" selected from many individual solvers on a given puzzle for being right in the middle of solve performance on that puzzle. 

#### Scatterplots for Individual Features vs IS2 Solve Times, with Associated Feature Distribution Density Plots (FDPs)

#### *Grid Features*

**<h4>Figure 11. Number of Answers**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/2f2a0c95-5798-426b-8be4-16b7a7e4db07)
*<h5>Individual Solver 2 (IS2) solve times and '# Answers' had a moderately strong negative correlation for 15x15 puzzles (r= -.47).<br>
Global Median Solver (GMS) correlation strength on the same set of 15x15 puzzles was stronger (r = -.55).<br>*

*Most of the strength of the all 15x15 puzzles correlation (black) was related to the large leftward shift in the FDP for the two most difficult puzzle days (Fri and Sat). '# Answers' was strongly negatively correlated with 'Average Answer Length' (see Fig. 14) and measures of answer rarity (e.g., 'Freshness Factor'; see Fig. 20). Thus, when puzzles were difficult (Fri and Sat), this fewer answers/more long answers combination meant more answers that were rarely encountered/unique. Within the most difficult puzzle days (Fri and Sat) moderately strong correlations of the same sign (-) as the overall 15x15 puzzles correlation were seen, emphasizing this relationship. Moreover, relatively strong correlations of the reverse sign (+) were seen for the early-week puzzle days (Mon-Wed). This finding suggests that, below a particular per-clue/answer difficulty threshold mostly only attained in later-week puzzles, the time penalty incurred by having to read relatively more clues was greater than the time savings from encountering relatively fewer longer answers.*              

**<h4>Figure 12. Number of Open Squares**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/1199318f-ad4e-467b-82f6-75b1ed48f46b)
*<h5>IS2 solve times and '# Open Squares' had a moderately strong positive correlation for 15x15 puzzles (r= .5).<br>
GMS correlation strength on the same set of 15x15 puzzles was stronger (r = .56).<br>*

*'# Open Squares' is a proprietary measure from XWord Info that counts all white squares that are *not* bordered by black squares. Most of the strength of the all 15x15 puzzles correlation (black) was related to the large rightward shift in the FDP for the two most difficult puzzle days (Fri and Sat), with nearly all 15x15 puzzles with >~80 open squares falling on those days. '# Open Squares' was strongly negatively correlated with '# Answers' (see Fig. 11) and strongly positively correlated with 'Average Answer Length' (see Fig. 14). For difficult puzzle days (Fri and Sat), these relationships translated to longer answers that were also more difficult. As with '# Answers' for this solver, the strongest within-puzzle day correlation of the same sign as the all 15x15 puzzles correlation (+) was seen for the most difficult puzzle day (Sat). This indicates that there may have been an overall difficulty threshold in play for this feature to have a large impact on solve times, though weaker positive correlations were seen for all puzzle days. Because nearly all puzzles with >~100 '# Open Squares' were on Saturday, however, it is challenging to distinguish a predominately puzzle difficulty threshold effect from a feature value range one.*   
    
 **<h4>Figure 13. Number of Black Squares**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/a71acb75-2c39-42ac-9479-b621415e076c)
*<h5>IS2 solve times and '# Black Squares' had a weak-to-moderate negative correlation for 15x15 puzzles (r= -.32).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = -.36).<br>*

*Most of the strength of the all 15x15 puzzles correlation (black) was related to the large leftward shift in the FDP for the two most difficult puzzle days (Fri and Sat), with nearly all 15x15 puzzles with <~32 black squares falling on those days. '# Black Squares' was strongly negatively correlated with both '# Open Squares' (see Fig. 12) and 'Average Answer Length' (see Fig. 14). So an increase in '# Black Squares' meant shorter, easier answers and a faster solve on average. Within Saturday a relatively strong correlation of the same sign as the all 15x15 puzzles correlation (-) was seen, emphasizing these dynamics. All other puzzle days showed negative correlations of variable strength for this solver, ranging from weak to moderate strength. This raises the possibility that there is a effect of '# Black Squares', within the feature value range of a given puzzle day, that scales to some degree with puzzle difficulty and may be of use in predictive modeling.*

**<h4>Figure 14. Average Answer Length**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/9ed11bac-ca86-4266-90b8-aa7925b10762)
*<h5>IS2 solve times and 'Average Answer Length' had a moderately strong positive correlation for 15x15 puzzles (r= .56).<br>
GMS correlation strength on the same set of 15x15 puzzles was stronger, reaching the level of strong correlation (r = .66).<br>*

*The moderately strong all 15x15 puzzles correlation was related to the large rightward shift in the FDP for the two most difficult puzzle days (Fri and Sat). Saturday also showed a relatively strong positive correlation across a wide range of feature values, with 'Average Answer Length' >~5.7 associated with mostly slower solves. As already discussed in the context of Figs. 11 and 12, 'Average Answer Length' was strongly negatively correlated with '# Answers' (see Fig. 11) and strongly positively correlated with measures of answer rarity (e.g. 'Freshness Factor; see Fig. 20). So it makes intuitive sense that as 'Average Answer Length' increased, particularly on difficult puzzle days, the answers themselves became more difficult and slowed down solve times even as they decreased in absolute number.* 

*Another interesting observation regarding this feature is that, unlike for the other grid features discussed thus far, the Thursday peak was well-differentiated to the right of those for the early-week puzzle days in the FDP. The peak of the Thursday solve time distribution for IS2 was also strongly right-shifted relative to Wednesday (see Figs. 2 and 4). Given that this feature showed a strong positive correlation to solve time, and that the same sign correlation was also was seen prominently for all late-week puzzle days (including Thursday), 'Average Answer Length' certainly holds some promise for having predictive value for the more difficult puzzles in the overall sample.* 

**<h4>Figure 15. Number of Cheater Squares**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/dc6c8515-45a0-4c07-a8c5-c254e0cfd29e)
*<h5>IS2 solve times and '# Cheater Squares' had a weak positive correlation for 15x15 puzzles (r= .13).<br>
GMS correlation strength on the same set of 15x15 puzzles was stronger (r = .2).<br>*

*Cheater Squares are black squares than can be removed without affecting the overall word count of the grid. These squares make construction easier (hence their name). It can be seen in the FDP that large numbers of them (>~10) almost exclusively appeared on the difficult puzzle days (Fri and Sat), which likely accounted for the (modest) positive correlation across all 15x15 puzzles. Saturday, with by far the widest feature value range of any of the 15x15 puzzle days, showed a moderate reverse sign (-) correlation. Each of the other 15x15 puzzle days except for Friday also showed some degree of reverse sign (-) correlation. This is not really at odds with the overall 15x15 positive correlation, since these squares are ultimately just black squares even if they facilitate tricky constructions for difficult puzzles. Add enough of them at a given puzzle difficulty level and they will reduce solve time simply by lowering the amount of fill. Incidentally, the reason cheater squares were only rarely seen in odd numbers is the NYT general requirement for grid symmetry.*

#### *Answer and Clue Content Features*

**<h4>Figure 16. Number of Fill-in-the-Blank Answers**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/a904822d-e834-47e8-a3de-e30e7e1a206c)
*<h5>IS2 solve times and '# Fill-in-the-Blank Answers' had a weak-to-moderate negative correlation for 15x15 puzzles (r= -.25).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = -.26).<br>*

*Most of the strength of this weak-to-moderate correlation for all 15x15 puzzles was related to the rightward shift in the FDP for Monday. Along with the easiest puzzle day employing the largest dose of '#Fill-in-the-Blank', the hardest puzzle day (Saturday) was also slightly left-shifted relative to the other 15x15 puzzle days. There were moderate correlations of the same sign (-) as the all 15x15 puzzles correlation for Friday and Saturday, and it does appear that feature values on the extremes were associated with impacts on solve time (slower times with very few '# Fill-in-the-Blank', faster times with relatively many). For the other puzzle days, the within-day correlations were weak. This suggests that the impact of this feature on solve times may interact with puzzle difficulty.* 
 
**<h4>Figure 17. Scrabble Average**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/b1b2fc9c-66f1-4ccb-991a-036bee173b5f)
*<h5>IS2 solve times and 'Scrabble Average' had a weak-to-nonexistent negative correlation for 15x15 puzzles (r= <-.01).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = -.02).<br>*

*'Scrabble Average' is another proprietary XWord Info measure, in which each letter in the answer grid is assigned its equivalent value in Scrabble. Since tile values in Scrabble increase with rarity of letter frequency in English texts, it would make sense that a higher value for this feature would be associated with *answers* of greater rarity. The more difficult 15x15 puzzle days (Thu-Sat) did show this tendency with (modest) positive correlations, suggesting that maybe there's a difficulty threshold for that relationship to manifest. Furthermore, 'Scrabble Average' had only moderate positive correlations with other more direct measures of answer rarity both across 15x15 puzzles (see Fig. 9) and specifically within the later-week puzzle days (see Supp. Fig. 1). Given that these more direct measures of answer rarity DID have strong positive correlations to solve times (see Figs. 18-20), this feature is a candidate to either be left out of predictive modeling entirely or to be combined with other answer rarity/difficulty measures to generate a novel predictive feature of slightly different flavor.*

**<h4>Figure 18. Number of Scrabble Illegal Answers**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/fcc2d999-ac1a-4acc-9f3d-f376ee8830c9)
*<h5>IS2 solve times and '# Scrabble Illegal' had a weak positive correlation for 15x15 puzzles (r= .13).<br>
GMS correlation strength on the same set of 15x15 puzzles was stronger (r = .18).<br>*

*'# Scrabble Illegal' answers is a proprietary measure of XWord Info that gets at answer rarity more directly than does 'Scrabble Average'. Interestingly, the distributions for 15x15 puzzle days in the FDP were highly overlapping, other than a small leftward shift for Monday and Tuesday that likely accounted for the (modest) overall 15x15 puzzles positive correlation. '# Scrabble Illegal" had only moderate positive correlations with the most direct measures of answer rarity ('# Unique Answers' and 'Freshness Factor'; see Figs. 19 and 20), which was somewhat surprising to me. There were hints, particularly in the Monday and Saturday correlation plots, that this feature might have impacted solve times at the extreme low and high ends of its value range. However, taken together with the weak correlation to solve times shown by this feature, the findings here suggest that more non-standard vocabulary *alone* may not strongly signify or predict puzzle difficulty.*  
    
 **<h4>Figure 19. Number of Unique Answers**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/240c9507-b2e4-4beb-a594-0edf67ee15e8)
*<h5>IS2 solve times and '# Unique Answers' had a weak-to-moderate positive correlation for 15x15 puzzles (r= .31).<br>
GMS correlation strength on the same set of 15x15 puzzles was stronger, reaching the level of moderate positive correlation (r = .4).<br>*

*<h5>A unique answer is defined here as one that does not appear in any other NYT crossword puzzle in either the Shortz or pre-Shortz eras (either before or after the puzzle release date). The strength (albeit moderate) of the all 15x15 puzzle day correlation was related to the easiest puzzle day (Monday) having a leftward shift in the FDP while the most difficult puzzle days (Fri and Sat) had rightward shifts. Though mostly of the weak-to-moderate variety, same sign (+) correlations relative to the all 15x15 puzzles one were seen on all puzzle days except for Friday. Across puzzle days, puzzles at the high end of a given day's feature value range can be seen to associate with slower solves. Thus, although uniqueness is perhaps an overly stringent criterion to capture answer unusualness, there may still be a signal useful for prediction at the high end of the feature value range that scales with puzzle difficulty.*

**<h4>Figure 20. Freshness Factor**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/e735ecac-eeba-48c0-b40a-5ce308059719)
*<h5>IS2 solve times and 'Freshness Factor' had a moderately strong positive correlation for 15x15 puzzles (r= .57).<br>
GMS correlation strength on the same set of 15x15 puzzles was considerably stronger, reaching the level of strong correlation (r = .67).<br>*

*<h5>'Freshness Factor' is another proprietary XWord Info measure that assesses the aggregate relative novelty of all answers in a given crossword puzzle as compared to those in all other crossword puzzles in the NYT archive. The much stronger correlation to IS2 raw solve times as compared to that for '# Unique Answers' suggests that there's much to be gained by taking a graded, as opposed to all-or-none, approach in assessing answer rarity. Overall, this feature had the strongest correlation with IS2 solve times of any grid, clue or answer feature evaluated (but see Fig. 22 for a past performance feature with a stronger correlation to raw solve times).* 

*Additionally, with potential relevance to predictive modeling, the 15x15 puzzle days peaked in this measure (seen in the FDP) in relatively close concordance to the by day peaks in raw solve times (see **Figs. 2 and 4**) for IS2. The only other puzzle feature coming close to this degree and concordance of peak separation was 'Average Answer Length' (see Fig. 14), though 'Freshness Factor' showed a Monday-Tuesday separation more in line with the solve time peaks separation for those two easy puzzle days. The positive correlation for this feature was also seen within each of the individual puzzle days, though more strongly for the later-week puzzle days. The greater strength for the later-week puzzle days suggests both that there may have been a puzzle difficulty interaction and that there may have been more of an effect above a feature value of ~45, where only Thu-Sat had a significant number of puzzles. Saturday had both one of the strongest within-day (15x15) correlations and also the widest range of feature values of any individual puzzle day. Nearly every puzzle with a feature value >60 was on that day, and nearly all were associated with slower solves. The observations discussed here lead me to believe that 'Freshness Factor' will be the most useful puzzle feature evaluated presently in terms of predictive modeling of solve performance.*

**<h4>Figure 21. Number of Wordplay Clues**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/8d96b322-7faa-4ef6-8062-c5198252ab34)
*<h5>IS2 solve times and '# Wordplay Clues' had a moderate positive correlation for 15x15 puzzles (r= .31).<br>
GMS correlation strength on the same set of 15x15 puzzles was substantially stronger (r = .44).<br>*

*<h5>'# Wordplay' clues is an (admittedly) somewhat subjective measure that I have manually evaluated and calculated clue-by-clue across (most of) the entire puzzle sample completed by IS2. The FDP for this feature had some interesting properties, including the clear result that late-week (Thu-Sat) puzzles indeed had a larger allocation of 'trickier' clues than early-week puzzles. There was also a prominent leftward shift for Monday puzzles, though with a strong second peak aligned with the Tuesday peak. Taken together, these early and late-week distribution offsets were related to the moderate overall positive correlation across all 15x15 puzzles. Only the early-week 5x15 puzzle days (and Sunday) showed any semblance of a (+) correlation, with the rare puzzles at the high end of those days' feature value ranges associating with slower solves. '# Wordplay' may have some value to predictive modeling of solve times, though possibly more so for the easy puzzle days when outlier feature values occur.* 

**<h4>Figure 22. Recent Performance Baseline (RPB)**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/0bfef8b7-930e-4457-981d-52fc710a5a32)
*<h5>IS2 next raw solve time and IS2 Recent Performance Baseline (RPB) had a strong positive correlation on 15x15 puzzles (r= .73).<br>
GMS next raw solve time and GMS RPB correlation strength was stronger, reaching the level of very strong correlation (r = .87).<br>*

*<h5> Next raw solve time and RPB Correlation Strength by Solver (IS2 or GMS) and Puzzle Day:*<br>
*IS2: Sun: .54, Mon: .47, Tue: .50, Wed: .43, Thu: .37, Fri: .40, Sat: .42*<br>
*GMS: Sun: .57, Mon: .61, Tue: .48, Wed: .42, Thu: .38, Fri: .42, Sat: .25*<br>

*<h5>The all 15x15 puzzles correlation for this feature was considerably stronger than that for any puzzle feature (**Figs. 11-21**). The implication is that non-decay-time weighted IS2 recent past performance (RPB over the 10 day-specific puzzles previous to a given solve) will likely have more predictive value for the next IS2 raw solve time than any single puzzle, clue or answer feature.* 

*Not all puzzle days were created equally, however, with regard to correlational strength (and, potentially, predictive power) of RPB and next raw solve time. Monday (r=.47) and Tuesday (r=.50) having higher correlations relative to the other 15x15 puzzle days was unsurprising, given how few "degrees of freedom" there were in the easiest puzzles. Monday and Tuesday had the highest and second highest 15x15 puzzle day correlations between RPB and next raw solve time for all 3 solvers (GMS, IS1, IS2). On the other side of the spectrum, the puzzle day with the lowest correlation for IS2 was Thursday (r=.37). This was notable because Thursday came in as the day with the lowest correlation by a large margin (r=.18) for IS1 (see analysis linked in Introduction) as well as the second lowest correlation of any puzzle day for the GMS (.38). Thus, variability in performance on that puzzle day due to outsized heterogeneity of puzzle difficulty and gimmickry may generalize across the solver pool. Thursday puzzles had a large degree of heterogeneity, with nearly all puzzles on that day involving a "trick" of some variety (including rebuses of various flavors; see Supp. Fig. 4).* 

*For the GMS, Saturday (r=.25) stood out as having a particularly low correlation between RPB and the next raw solve time. In contrast, correlations for both IS1 and IS2 on this most difficult puzzle day were actually higher than for the other late-week puzzle days (Thu and Fri). My suspicion is that this largely related to the volatility of the Saturday solver pool that the GMS was drawn from. As the most difficult puzzle day virtually every week, the Saturday solver pool may have had both a lower N to draw from for each individual puzzle as well as a much more variable roster of puzzle completers than the other puzzle days. Substantial contributions to the relatively low Saturday correlation for the GMS may have also been due to the heterogeneity of Saturday puzzles (ie, characteristically wide feature value ranges) and the high likelihood of middle-of-the-pack solvers getting "stuck" for extended stretches on one or several tough clues or answers.*

 # Supplementary Figures

**<h4>Figure S1. IS2 10-Puzzle Solve Time Moving Averages Adjusted by GMS Performance, by Puzzle Day** 

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/e6b7684c-76a5-4a2b-a9c6-41244fa78e61)
*<h5>For each puzzle completed by IS2, % difference for the raw solve time from the global median solve time (GMST) was computed. The 10-puzzle moving average of this difference was then plotted, per puzzle day, by completion date. The volatility present in the raw solve times (see **Fig. 2 and Fig. 4**), including the upward spike in Q2-early Q3 2023, was still mostly present in these adjusted data plots, indicating that this volatility was due to factors other than by chance stretches of puzzles with substantially greater or lesser difficulty per puzzle day.*

**<h4>Figure S2. Solve Time Overview by Puzzle Day: Violin Plots With Swarm Plot Overlay for First Solve Interval (2018-2019)**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/0577ca56-e490-45d3-832e-7d5463aeeb85)
*<h5>Median[IQR] solve time (m), per puzzle day, for 2018/19 solve interval:*<br>
*2018/19: Sun: 69.3[59.4-82.2], Mon: 10.3[8.7-11.8], Tue: 15.4[11.2-24.5], Wed: 21.5[14.9-34.2], Thu: 43.4[39.6-63.8], Fri: 33.3[30.7-48.5], Sat: 52.0[41.7-55.7]*<br>

**<h4>Figure S3. Correlation Heatmapping of IS2 Individual Puzzle Performance vs Grid, Answer and Past Performance Features by Puzzle Day (15x15 Puzzle Days)**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/075c68ab-3ede-4a24-8d9c-7899f37194a0)
*<h5>N's ranged between 153 (Mon) and 177 (Fri) per 15x15 puzzle day*

**<h4>Figure S4. Number of Rebus Squares vs IS2 Solve Time by Puzzle Day**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/afd7e7fc-56d9-4392-a906-0f2701c8e88d)
*<h5>Only Thursday had an appreciable '# Rebus Squares' for IS2 solves. Rebus squares are those that must be filled with more than one letter, number or symbol for a given puzzle to be solved. There was a weak positive correlation for IS2 and a moderate one for GMS for Thursday, though a caveat is that the very large number of 0 rebus puzzles makes these correlations hard to interpret (ie, these are not exactly continuous distributions).*<br>

*Correlation Strength by Puzzle Day: IS2: Thu: .17; GMS: Thu: .26* 

**<h4>Figure S5. Number of Circled Squares vs IS2 Solve Time by Puzzle Day**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/313b02a1-b8ff-4e47-89c3-c92a7fb6f98c)
*<h5>Circled squares were virtually non-existent in the tougher (Fri and Sat) puzzles. The modest negative correlation seen across all 15x15 puzzle days (-.11) is attributable to the fact that most 15x15 puzzles with circles appeared early in the week. The smattering of puzzles with circles on Sunday almost all fell in the middle of the solve time range regardless of '# Circles', indicating that this feature didn't likely have a major impact on solve times.*

**<h4>Figure S6. Number of Shaded Squares vs IS2 Solve Time by Puzzle Day**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/caccbcc8-c8c3-48bd-a9c1-9b1d0a6616ce)
*<h5>Shaded squares, like circled squares, were virtually non-existent in the tougher (Fri and Sat) puzzles. Also like with circled squares, their function is to reveal a puzzle theme and their presence may provide assistance to solvers on clues in which they are embedded. Most puzzles with shaded squares were within the bottom third of IS2 15x15 puzzle solve times, most likely due to shaded squares almost exclusively showing up only in early week puzzles. Also as with '# Circles', the smattering of Sunday puzzles almost all fell in the middle of the solve time range regardless of '# Shaded Squares', indicating that this feature also isn't likely having a major impact on solve times.* 










