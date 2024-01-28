
# Exploratory Data Analysis of Individual Solver 2 (IS2) Performance on the New York Times Crossword Puzzle

## Introduction

### Project Overview
This summary reports on exploratory data analysis (EDA) of an individual solver's (Individual Solver 2; IS2) performance over a large subset of nearly 6 years (Mar. 2018 - Jan. 2024) of the [New York Times (NYT) crossword puzzle](https://www.nytimes.com/crosswords). Included are visual and statistical descriptions of trends in IS2 solve times across this period, performance relative to the 'Global Median Solver' (GMS; see next section), and the relationship between IS2 performance and a number of variables. These variables included properties of the puzzle grids (e.g., number of answers, number of black squares), clues and answers (e.g., frequency of wordplay in clues, aggregate rarity of answers in a puzzle), environment (e.g., time of day a puzzle was completed), constructor identity, and puzzle day-specific recent past performance prior to a given solve. This EDA led to identification of a set of features that hold promise as useful inputs to a predictive model of IS2 future performance.

Without access to two specific data sources this project would not have been possible. The first, [XWord Info: New York Times Crossword Answers and Insights](https://www.xwordinfo.com/), was my source for data on the puzzles themselves. This included a number of proprietary metrics pertaining to the grids, answers, clues and constructors. XWord Info has a contract with NYT for access to the raw data underlying these metrics, but I unfortunately do not. Therefore, I will not be able to share raw or processed data that I've acquired from their site. Nonetheless, [Jupyter notebooks](https://jupyter.org/) with all of my Python code for analysis and figure generation can be found [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/tree/main/notebooks)). The second, [XWStats](xwstats.com), was my source for historical solve time data for both IS2 and the GMS.

Similar analyses to those reported here for IS2 were performed on another individual's (IS2) data over a comparable sample size and timespan, and are summarized [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1?tab=readme-ov-file#readme).

### The Global Median Solver (GMS)

Many analyses included in this summary compare IS2 performance to that of the GMS over the set of all IS2 solves. My extensive summary analysis of GMS performance over a 6+ year timeframe (2018-2024) can be found [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Global-Median-Solver?tab=readme-ov-file#readme). XWStats (Matt) determines the global median solve time (GMST) for every individual puzzle from a pool of ~1-2K individual solvers from whom he has (with their consent) acquired personal solve data, via NYT. Though Matt adopted the term "global" to describe this solver sample per-puzzle, it likely skews faster than the overall population of solvers. The reasons for this assumption are twofold; only solvers who actually complete a given puzzle are included in its sample, and each sample contains only solvers motivated enough by the prospect of improvement to track their own progress to begin with. 

GMSTs improved on each puzzle day over the complete set of puzzles (N=2,218) issued between January 1, 2018 and January 27, 2024 (**Figure 1**). This improvement was fairly dramatic in the first few years for some puzzle days (most prominently for Sun), and graded improvement continued for each puzzle day until the end of the sample period (top panel). The 2-year interval density plots of raw solve time distributions (bottom panels) show that performance on individual puzzle days became more consistent over time (higher peaks with narrower distributions). Because I did not have access to the raw solver data from which the GMSTs were drawn, however, it was not possible to disentangle improvement and increased consistency for individual "early adopters" of Matt's tracking software versus stronger solvers joining the solver pool over time. Note also that GMS performance was tracked in my analyses by puzzle issue date, as I did not have access to GMS puzzle completion dates. It's reasonably safe to assume, however, that the GMS (a different individual solver for most puzzles, presumably) solved in approximately the sequence of puzzle issue. IS2 performance, in contrast, was tracked by puzzle completion data since I *was* able to obtain completion timestamps for my own solves with Matt's assistance.  

**Figure 1. GMS Solve Time Overview by Puzzle Day: 10-Puzzle Moving Averages and Distributions of Raw Values**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/b1f6464c-b57f-402b-a2b7-8f44716f2350)
*<h5>GMS Final (as of Jan. 27, 2024) 10-puzzle moving average of solve time (m), per puzzle day:*<br>
*Sun: 28.8, Mon: 5.7, Tue: 7.7, Wed: 11.4, Thu: 15.2, Fri: 17.3, Sat: 21.2*<br>



## Results
### Individual Solver 2 (IS2) Performance Over Time

IS2 solved N = 1,071 puzzles in the sample period: 89 (8.3%) in 2018, 9 in 2019 (.8%), 282 in 2020 (26.3%), 28 (2.6%) in 2021, 79 (7.4%) in 2022, and 584 (54.5%) in 2023/24 (through Jan. 28, 2024). The total solve time for IS2 was 17.1 days (2018: 2.2 days; 2019: .14 days; 2020: 5.1 days; 2021: .25 days; 2022: .97 days; 2023/24: 8.4 days). The total solve time for the GMS over this same set of puzzles was 14.2 days. 

IS2's per puzzle day 10-puzzle moving averages across the sample period are shown in **Figure 2** (top panel). The first 5 years were characterized by long periods of little solve activity (flat stretches in lines) punctuated by rapid and dramatic improvements across puzzle days during months-long bursts of activity. There was a short-term, spiked increase in solve times across puzzles days when solving resumed after a long layoff in Q2 2023. Then, from late Q3 2023 through the end of the sample period, IS2 showed dramatic improvement across puzzle days relative to even pre-spike baselines. **Supplementary Figure 1** shows that the volatility of IS2's per puzzle day solve times in 2023 was *not* likely due to chance stretches of puzzles with higher or lower than usual median difficulty (as determined by GMS performance on the same puzzle set). Improvement over the last ~4 months of the sample period was especially apparent on the more difficult puzzle days (Thu-Sun). The leftward shift in peaks for the by day solve time distributions in the 2023/2024 density plot (**Fig. 2**, bottom right) clearly demonstrates this recent improvement in solve form. Additionally, overall distribution widths narrowed considerably across solve intervals for early week (Mon-Wed) puzzle days. This indicates increased consistency of solve performance over time for IS2.    

**Figure 2. Solve Time Overview by Puzzle Day: 10-Puzzle Moving Averages and Distributions of Raw Values**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/f30407a3-d70c-4918-8ca8-59432e58f52e)
*<h5>IS2 Final (as of Jan. 27, 2024) 10-puzzle moving average of solve time (m), per puzzle day:*<br>
*Sun: 18.7, Mon: 5.0, Tue: 7.0, Wed: 9.2, Thu: 19.4, Fri: 13.5, Sat: 22.4*<br>


###

**Figure 3** shows IS1's solve time performance trajectory in violin plots with swarm plot overlays, broken out by 1-year solve date intervals. These representations may be somewhat easier to digest than the line plots in **Fig. 2**, as they remove the compressing effect of the long intervals with minimal solve activity. They also have the advantage of providing a clear visual sense of the number of solves and distribution shape, per interval. Violin plots show both the range (vertical extent) and distribution characteristics (width as it varies across the y-axis range) for each puzzle day, per solve interval. Black lines on the violin plots demarcate solve time quartiles per puzzle day. Swarm plot overlays per puzzle day show individual puzzle raw solve times. The narrow geometries of the later week violin plots relative to the earlier week ones correspond to greater relative performance variability on those solve days. This phenomenon will be discussed in the final section of the summary in the context of correlation between past and future performance and prospects for predictive modeling. 

**Figure 3. Solve Time Overview by Puzzle Day: Violin Plots With Swarm Plot Overlay**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/23363b58-4a67-4993-bdeb-87aea3b4e63d)
*<h5>Median[IQR] solve time (m), per puzzle day, per solve interval:*<br>
*2018/19: Sun: 69.3[59.4-82.2], Mon: 10.3[8.7-11.8], Tue: 15.4[11.2-24.5], Wed: 21.5[14.9-34.2], Thu: 43.4[39.6-63.8], Fri: 33.3[30.7-48.5], Sat: 52.0[41.7-55.7]*<br>
*2020-22: Sun: 43.0[36.6-52.4], Mon: 7.1[5.9-8.2], Tue: 10.6[8.7-12.6], Wed: 14.0[11.5-20.0], Thu: 25.0[18.2-31.0], Fri: 26.3[18.4-32.0], Sat: 34.8[28.0-50.4]*<br>
*2023/24: Sun: 32.3[26.5-40.9], Mon: 5.7[4.8-6.5], Tue: 7.4[6.8-8.5],   Wed: 11.6[9.7-14.2], Thu: 20.0[15.9-25.6], Fri: 18.9[14.7-25.0], Sat: 26.2[20.7-36.2]*<br>

###
Because over half of IS2' total solves (n=584) came in 2023-2024, and there was such rapid and dramatic improvement over the latter ~1/3 of that time range, zoom-in and 2-interval partition of this time range is depicted below in **Figure 4**. IS2 had n=337 solves in the final 3.5 months of the time range, spread roughly equivalently across puzzle days. The dramatically improved solve performance (Sat median solve time, for ex., dropped from 38.5 to 23.3 minutes) during this period was likely driven by the high volume of solving in a condensed period of time.    

**Figure 4. Solve Performance in 2023-2024**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/5a553512-94d0-489b-9921-212e7d83a5af)
*<h5>Median[IQR] solve time (m), per puzzle day, per solve interval:*<br>
*Apr 2023-Sept 2023: Sun: 41.2[32.6-47.1], Mon: 5.9[5.5-6.7], Tue: 7.7[6.9-8.9], Wed: 13.2[10.6-14.9], Thu: 26.4[18.9-32.1], Fri: 24.2[18.0-32.0], Sat: 38.5[26.7-46.1]*<br>
*Oct 2023-Jan 2024:  Sun: 27.8[23.8-33.6], Mon: 5.4[4.7-6.3], Tue: 7.2[6.6-8.4], Wed: 10.1[8.4-12.1], Thu: 17.0[13.9-21.0], Fri: 16.9[12.8-22.6], Sat: 23.3[17.4-31.3]*<br>



### Individual Solver 2 (IS2) Performance Vs Global Median Solver (GMS) 

The next series of figures directly compare IS2 solve performance to that of the GMS over the same puzzle set. For these analyses, IS2 solves were broken into 2 solve intervals: pre-2023 (n=487; 45.5% of total solves; 2023/24: n=584; 54.5%). Per puzzle day, in the figures relevant to these analyses, pre-2023 solves are represented by lighter-colored points and regression lines and 2023/24 solves by darker-colored ones. 

**Figure 5** shows per-puzzle day scatterplots of raw GMSTs (x-axis) versus raw IS2 (y-axis) solve times. Points falling on the dashed diagonal line represent identical raw solve times for IS2 and GMST on a given puzzle. Points above and below this line represent "wins" for the GMS and IS2, respectively. IS2 win % across all puzzle days improved greatly from the pre-2023 (28.7%) to 2023/24 interval (50.0%). Win %s for IS2 also increased dramatically for most puzzle days in 2023/24, including a >2x increase for both Tuesday (34.6% to 71.6%) and Saturday (13.7% to 30.2%). The lowest IS2 win % for both time intervals was for Saturday, and Monday yielded the highest and second highest IS2 win %s in the pre-2023 and 2023/24 intervals, respectively (48% and 65%). The mean magnitude of performance advantage for the GMS over IS2 also decreased considerably in the more recent solve interval for all puzzle days together (6.1 to 2.2 minutes), as well as for all individual puzzle days (with IS2 gaining the advantage by this measure from Mon-Wed). Finally, per puzzle day regression lines show that there was a relatively high degree of correlation for raw solve times between IS2 and GMST (range across individual puzzle days and solve intervals: .54-.82). The next figure addresses this correlation in a way that is normalized for recent (prior to a give solve) baseline performance, per solver. This is a particularly useful for IS2, since this solver solved many older puzzles in 2023-2024. Thus, the GMS was earlier on "their" own improvement curve when solving the same puzzles.   

**Figure 5. IS2 vs GMS: Comparison of Raw Solve Performance by Puzzle Day and Solve Interval**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/5c4e6b84-59d9-44c6-a26a-4c4ba20e3de6)
*<h5> Win % for IS2 vs GMS, by IS2 solve interval:*<br>
*pre-2023: All: 28.7, Sun: 24.2, Mon: 48.1, Tue: 34.6, Wed: 29.1, Thu: 20.8, Fri: 22.2, Sat: 13.7*<br>
*2023/24:  All: 50.0, Sun: 48.2, Mon: 65.7, Tue: 71.8, Wed: 57.5, Thu: 40.2, Fri: 41.9, Sat: 29.8*<br>

*<h5> Mean(stdev) Solve Time Difference (m) for IS2 vs GMS, by IS2 solve interval (negative denotes faster for IS2):*<br>
*pre-2023: All: 6.1(10.5), Sun: 9.6(13.6), Mon: .64(2.3), Tue: 1.8(3.4), Wed: 3.4(6.1), Thu: 8.7(11.1), Fri: 7.9(11.8), Sat: 15.3(14.8)*<br>
*2023/24:  All: 2.2(8.1), Sun: 1.1(8.7), Mon: -.15(1.2), Tue: -.67(1.2), Wed: -.14(3.3), Thu: 2.7(7.0), Fri: 3.1(8.6), Sat: 7.6(12.7)*<br>

###
Along with comparison of raw solve performance between IS2 and GMS, the degree to which the same puzzles were *relatively* difficult for the two solvers was addressed. Per solver (IS2 or GMS) each raw solve time was taken as a % difference from a decay-time weighted average of the *previous* 20 puzzles solved on the same puzzle day ('Recent Performance Baseline'; RPB). These RPB-adjusted solve times were then plotted against each other on a per puzzle day and per solve period basis (**Figure 6**). Points falling in the lower left ("relatively easy for both solvers") and upper right ("relatively hard for both solvers") quadrants represent concordance of relative difficulty for a given puzzle. The most common outcome across puzzle days for both solve periods was "relatively easy for both solvers" (pre-2023: 48.8%; 2023/24: 43.9%), and the second most common was "relatively hard for both solvers" (pre-2023: 24.8%; 2023/24: 26.9%).  

It's no surprise that "easy" concordance was more common than "hard" concordance, since solvers constantly improved/outperformed their RPB on a puzzle-to-puzzle basis. A substantial minority (~30%) of puzzles, however, were either relatively easy for IS2 and relatively hard for GMS or vice versa (lower right and upper left quadrants, respectively). Of the two discordant quadrants, "relatively easy for IS2 and relatively hard for the GMS" was slightly more common in both solve intervals across puzzle days (16.5% vs 10% and 16.3% vs 13%). The considerable % of puzzles falling into discordant quadrents suggests that environmental and puzzle-specific variables may affect different solvers in different ways. Starting in the next section, the focus will be on summarizing the effects of some of these variables on IS2 (and GMS) performance.    

**Figure 6. IS2 vs GMS: Comparison of Baseline-Adjusted Solve Performance by Puzzle Day and Solve Interval**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/e19132d2-50e0-4cb5-bcb7-5b5037a25d83)
*<h5> IS2-GMS Quadrant % by IS2 solve period:*<br>
*LL: Relatively Easy for Both IS2 & GMS/ UR: Hard for IS2 & GMS/ UL: Easy for GMS-Hard for IS2/ LR: Easy for IS2-Hard for GMS*<br> 
*pre-2023: All: 48.8/24.8/10.0/16.5, Sun: 52.5/23.0/9.8/14.8, Mon: 41.0/25.6/7.7/25.6, Tue: 43.8/27.5/15.0/13.8, Wed: 47.4/23.1/7.7/21.8, Thu: 53.5/25.3/8.5/12.7,<br> Fri: 51.6/24.2/14.5/9.7, Sat: 56.0/24.0/6.0/14.0*<br>
*2023/24:  All: 43.9/26.9/13.0/16.3, Sun: 45.9/29.4/9.4/15.3, Mon: 41.1/19.2/17.8/21.9, Tue: 47.3/23.0/16.2/13.5, Wed: 44.8/28.9/9.2/17.1, Thu: 42.3/31.8/10.6/15.3,<br> Fri: 45.3/25.3/15.8/13.7, Sat: 40.6/29.2/12.5/17.7*<br>

### IS2 Performance by Puzzle Constructor(s)

A high proportion of puzzles solved by IS2 (69.7%) were authored by either repeat individual constructors or repeat specific constructor teams (both referred to as "constructor" from here forward). This afforded the opportunity to evaluate which constructors IS2 tended, in a relative sense, to struggle against or do well against. Per constructor, the mean of % difference from puzzle day-specific recent performance baseline (RPB; see text section pertaining to **Fig. 6**) was computed. This measure allowed assessment of constructor difficulty adjusted for solver form at the time of a given solve and constructor past puzzle day heterogeneity. **Figure 7** shows heatmapping of IS2 performance using this normalized measure, along with GMS performance on the same set of puzzles, against the n=69 constructor(s) contributing >=4 puzzles over the sample period. While only 13.2% of constructor(s) contributed this many puzzles, this group contributed 41.5% of all puzzles solved by IS2.

Warmer colors (-%) in **Fig. 7** indicate that on average the solver was relatively fast against a given constructor; cooler colors (+%) indicate slower solves. Mean difference from RPB for IS2 solve time against different constructors ranged from -58.7% for "easiest constructor" (Brian Thomas) to +35.5% for "hardest constructor" (Kyle Dolan). The range for the GMS was considerably smaller, from -40.3% for "easiest constructor" (Nate Cardin) to +20.1% for "hardest constructor" (Peter A. Collins). "Hot" or "cold" constructors for IS2 tended to be relatively fast or slow, respectively, for the GMS. However, there was clearly a substantial degree of discordance in terms of specific order and some constructors stood out as being either "hot" for IS2 but "cold" for the GMS (e.g., Adrian Johnson, Trent H. Evans) or vice versa (e.g., Ruth Bloomfield Margolin, Will Nediger). 


**Figure 7. Heatmapping of IS2 and GMS Performance Against Individual Constructors**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/037d9088-7fa9-447f-ac8d-464699e42026)
*<h5>Constructor rankings are sorted by normalized IS2 relative solve speed. GMS values over the same set of puzzles are included for comparison.*<br>

The next correlational analysis was aimed at assessing the potential predictive value of IS2's baseline-adjusted past performance against specific constructors on their future performance against the same constructor. **Figure 8** shows this correlation between IS2 past performance (as mean % difference from RPB) against a given constructor (x-axis) and performance on the next solved individual puzzle by that constructor (y-axis). This analysis was restricted to only the n= puzzles by the constructor included in **Fig. 7** that were solved *after* >=3 previous puzzles by the same constructor (based on puzzle completion date for IS2, but issue date for GMS). There was a weak-to-moderate positive correlation for IS2 (r=.20), and a stronger one for GMS (r=.30). This weaker correlation for the individual solver relative to the GMS was also seen for IS1 (see link to analysis in Introduction). This disparity may have been due to the fact that performance for a single solver is inherently subject to more puzzle-to-puzzle variability than that of an "aggregate solver". Regardless, the evident positive correlations for all three solvers at relatively low puzzle n's provides optimism that including past performance vs constructor will have predictive value in the modeling phase.     

**Figure 8. IS2 and GMS: Past Performance Against Individual Constructors as "Prediction" of Next Puzzle Performance Against the Same Constructor**  

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/12283951-36f5-4344-8d1a-e38b090e410d)
<h5>Pearson correlation coefficient (r): IS2: .20, GMS: .30

### IS1 Performance by Completion Time of Day

Many external variables are likely to have an impact on individual solver performance, for the large majority of which data collection would be very difficult. Examples include data relevant to how tired, stressed, influenced by caffeine and other substances, or distracted by other sensory stimuli the solver was while working on a given puzzle. One external variable that we *are* fortunate to have data on (thanks, once again, to Matt at XWord Stats) is time of day at puzzle completion. **Figure 9** shows IS2's solve performance by hour of day, overall (black) and by puzzle day (by color). To control for day-specific puzzle difficulty, solve times are expressed as % difference from puzzle day-specific recent performance baseline (RPB).

The majority of IS2 solves occurred in the evening (65% after 6 PM and 37% after 9 PM). One interesting trend was that very few solves between 12-8 AM (3/80; 3.8%) were "extremely fast" (>=50% faster than day-specific RPB). In contrast, 58/493 (11.7%) solves between 8-11 PM qualified as "extremely fast". So while there was no striking overall relationship between solve time and hour of completion, IS2's top performances were ~3x more likely to come in the evening than late at night or in the early morning. Nonetheless, interpretation of this result is still difficult because puzzle *start* times were not available. Thus, it can't be distinguished with the available data whether IS2 was a better performer at night or simply finished easier puzzles before bedtime and left harder ones for morning completion. Another caveat is that all solve times were recorded with respect to the US Eastern Time Zone, and there is no indication for puzzles completed in other time zones.    

**Figure 9. Baseline-Adjusted Solve Times by Hour of Completion**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/e37c8714-c800-4cb4-bf55-2d4d2c80f252)
*<h5>Times are all US Eastern Time Zone, adjusted for Daylight Savings Time as necessary.*

### Correlations of IS2 Performance on Individual Puzzles to Puzzle-Specific Features and Recent Past Performance

Numerous potentially interesting features pertaining to puzzle grids, clues, and answers were obtained from XWord Info across the sample period. Features showing strong correlation to IS2 solve performance become strong candidates as input features for predictive modeling, in current forms and/or when combined in novel ways with other existing features. **Figure 10** shows correlation heatmapping separately for 15x15 puzzles (Mon-Sat) and 21x21 puzzles (Sun) for a subset of all measured features with distributions amenable to linear regression and correlation analysis (see **Supplementary Figure 2** for individual 15x15 puzzle day matrices). The Pearson correlation coefficient (r) captures linear correlation strength between a given feature and solve times (top row and leftmost column of correlation matrix; red indicates a strong positive correlation and green a strong negative correlation). The rightmost column/bottom row per matrix shows the correlation between IS2 solve times for individual puzzles and puzzle day-specific recent performance baseline (RPB). For both 15x15 puzzles and 21x21 puzzles, this (positive) correlation was stronger than any other measured feature correlation to IS2 solve time. This finding generates a prediction that recent (relative to a puzzle date to be predicted) solver form per puzzle day will be more predictive of performance on a novel puzzle than will be any individual grid, clue or answer feature. 

As can also be seen in the **Fig. 10** correlation matrices, a number of grid, clue and answer-related features correlated strongly with each other. For example, 'Average Answer Length' and 'Freshness Factor' showed a strong negative correlation. This relationship makes intuitive sense because 'Freshness Factor' is a measure of aggregate answer rarity for a given puzzle, and longer answers have a higher likelihood of being uncommon than shorter ones. Additionally, numerous features not selected for this analysis might still be useful in predictive modeling but either had non-continuous distributions (e.g., 0 or 1 for puzzles with normal vs non-standard symmetry) or pertain to a feature that is largely specific to only one or several puzzle days (e.g. Rebuses, Circles, Shaded Squares; see **Supplementary Figures 3-5**).   


**Figure 10. Correlation Heatmapping of IS2 Raw Solve Times vs Grid, Clue, Answer and Past Performance Features**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/c8b6f0cc-fc91-442e-96a3-ad9c9eafbecb)
*<h5>Correlation heatmaps derived from N=823 15x15 (left panel) and N=132 21x21 (right panel) puzzles solved by IS2 from 2020-2024.*

*Note on Inclusion Time Range*: As is clear in **Fig. 10**, RPB had the strongest correlation to individual solve times of any feature evaluated by a considerable degree. As such, there was a concern that shifts in baseline solve speed could overwhelm or mask correlations with puzzle-specific features. But normalizing raw solve times (e.g., with RPB) cancels out cross-puzzle day trends that I was interested in identifying prior to the modeling stage. As such, I arrived at a compromise in which I removed all solves from the first solve interval (2018/2019; n=98), which reduced baseline volatility in the solve pool to a considerable degree and allowed me to keep raw solve times as the y-axis variable across these analyses.*


###

**Figure 11** through **Figure 22** are companion figures to the correlation heatmapping shown in **Fig. 10**. These figures show, across all 15x15 puzzle days (black) and by-puzzle-day (colored), scatterplots of select features of interest vs IS2 raw solve times at the level of individual puzzles. A feature distribution density plot (FDP) shows puzzle day-specific trends in the distribution of each plotted feature. 

Though most features had at least a moderate correlation strength with IS2 solve times across all 15x15 puzzles, at the by-puzzle-day level these correlations were typically stronger for the more difficult puzzle days (Sat, in particular). Any feature showing a relatively strong correlation within the late week puzzles days is a strong candidate for having a causal impact on solve times in the modeling phase. Correlations robust enough to show through when many other variables are controlled for within a given puzzle day are likely to have a meaningful impact on solve times. Furthermore, there may be threshold values per feature below/above which that feature's impact is not significant in comparison with the effects of solver aptitude (see discussion above about **Fig. 10**, and also see **Fig. 22**). Because late week puzzle days almost uniformly had considerably wider ranges of feature values than earlier week puzzle days (compare per day widths in the FDPs or x-axis extents in the scatterplots), effects apparent on those late week days would be absent or severely clipped by the limited ranges on the early week days. Finally, early week puzzles may also simply not be difficult enough overall for given features (especially grid features, as a clue is only as difficult as the answer content that it houses) to have discernable impacts on solve times.    

Each figure caption for **Figs. 11-22** compares the correlation strength for a given feature for IS2 with that for the global median solver (GMS) over the same set of puzzles. While GMS correlations were uniformly directionally the same as for IS2, they were also uniformly *stronger* than those for IS2. This relative strength was likely related to the more variable per day baseline solve performance of IS2 relative to the GMS (**see Figs. 1-4**), which in turn relates to one being a single human subject to puzzle-to-puzzle variability in many aspects and the other being a "mathematical entity" selected from many individual solvers on a given puzzle for being right in the middle of solve performance on that puzzle.


#### Scatterplots for Individual Features vs IS2 Solve Times, with Associated Feature Distribution Density Plots (FDPs)

#### *Grid Features*

**Figure 11. Number of Answers**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/fdccd53f-28a4-4bef-90ab-28f3206e1c16)
*<h5>Individual Solver 2 (IS2) solve times and '# Answers' had a moderately strong negative correlation on 15x15 puzzles (r= -.48).<br>
Global Median Solver (GMS) correlation strength on the same set of 15x15 puzzles was slightly stronger (r = -.55).<br>*

*More answers typically meant shorter answers (see correlation matrices above), and shorter answers tended to be more common/easier answers (see 'Average Answer Length' and 'Freshness Factor' analyses below). Aligned with this relationship, the FDP for this feature shows that the toughest puzzle days (Fri and Sat) tended to have the fewest answers. The relatively strong *positive* correlations seen for Monday and Wednesday (also seen for Mon for IS1 and GMS) suggest that, below a particular per-clue/answer difficulty threshold, merely having to read more clues to solve the puzzle may penalize the solver more they are rewarded for avoiding longer answers.*

**<h4>Figure 12. Number of Open Squares**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/234e533f-921e-4df6-92e1-3066599192dd)
*<h5>IS2 solve times and '# Open Squares' had a moderately strong positive correlation on 15x15 puzzles (r= .51).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = .57).<br>*

*'# Open Squares' is a proprietary measure from XWord Info that counts all white squares that are *not* bordered by black squares. '# Open Squares' was strongly positively correlated to 'Average Answer Length' (see matrices above), so it makes sense that a greater '# Open Squares' was also positively correlated with solve times. The FDP shows that the most difficult puzzle days (Fri and Sat) had a rightward shift in '# Open Squares' relative to the easier 15x15 puzzle days. A large amount of the overall 15x15 correlation for IS2 appears to be accounted for by these more difficult puzzles with large numbers (>~80) of open squares.* 

**<h4>Figure 13. Number of Black Squares**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/eb14d2f8-91ec-41b9-953b-a999a9ebcb8d)
*<h5>IS2 solve times and '# Black Squares' had a weak-to-moderate negative correlation on 15x15 puzzles (r= -.32).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = -.35).<br>*

*This relationship was essentially the opposite (albeit a weaker form) of that between solve times and '# Open Squares' (more black squares = shorter answers = easier answers). Both Friday and Saturday were strongly left-shifted in the FDP, which suggests that most of the overall 15x15 puzzle negative correlation was due to the most difficult days tending to have relatively few black squares. For IS2, varied in strength but each showed at some some degree of negative correlation. The day with the widest range of values (Sat) had a negative correlation nearly as strong as the overall 15x15 correlation, which for reasons discussed in the preface to this section makes this feature an interesting candidate for substantial impact in predictive modeling.*

**<h4>Figure 14. Average Answer Length**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/e86e5df7-b8b5-4e2e-b2e8-da832e51f980)
*<h5>IS2 solve times and 'Average Answer Length' had a moderately strong positive correlation on 15x15 puzzles (r= .58).<br>
GMS correlation strength on the same set of 15x15 puzzles was considerably stronger, reaching the level of strong correlation (r = .67).<br>*

*This finding was consistent with other grid feature relationships to IS2 solve times, which makes sense since longer answers meant more multiword and relatively-rare answers (see correlation matrices above and **Figs. 18-20**). This positive correlation was apparent for the large majority of the individual puzzle days and, as was typical for grid features for IS2, it was strongest for Saturday. As with '# Answers', Monday stood out in showing the reverse correlation sign relative to the set of all 15x15 puzzles. Given that this feature and '# Answers' are themselves highly negatively correlated (see **Fig. 10**), it makes sense that an easy puzzle day would again serve as the exception that proves the rule. Longer answers that are still easy may increase solver speed in the aggregate by reducing the amount of clues consumed needed for a solve, without a counterbalancing 'difficulty penalty' that might occur with longer answers on later puzzle days.* 

**<h4>Figure 15. Number of Cheater Squares**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/f6ede496-94e2-4990-b803-d3aa6d347a25)
*<h5>IS2 solve times and '# Cheater Squares' had a weak positive correlation on 15x15 puzzles (r= .13).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger, reaching the level of a moderate positive correlation (r = .20).<br>*

*Cheater Squares are black squares than can be removed without affecting the overall word count of the grid. These squares make construction easier (hence their name). It can be seen in the FDP that large numbers of them (say, >10) almost always appeared on the difficult puzzle days (Fri and Sat), which accounts for the (modest) positive correlation across all 15x15 puzzles. There were, however, relatively strong reverse sign (negative) correlations seen within Monday and Saturday, and weaker ones seen on the other puzzle days. This raises the possibility of diminishing returns on '# Cheater Squares'; they may help make constructions "trickier" up to a point, but beyond that point on balance they speed solvers up simply by lowering the number of fill squares (a la a high '# Black Squares'). Incidentally, the reason cheater squares were only rarely seen in odd numbers is the NYT general requirement for grid symmetry.*

#### *Answer and Clue Content Features*

**<h4>Figure 16. Number of Fill-in-the-Blank Answers**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/a32d4bc6-3612-408f-9475-c24f81c6de88)
*<h5>IS2 solve times and '# Fill-in-the-Blank Answers' had a weak-to-moderate negative correlation on 15x15 puzzles (r= -.25).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = -.26).<br>*

*Taken together, the FDP and scatterplots indicate that most of the strength of this correlation was due to the easiest puzzles (note the rightward FDP peak shift for Mon, even relative to Tue) employing a heavy dose of FITB answers. It's also noteworthy that the most difficult puzzle days (Fri and Sat) clearly made less use of FITB answers than the other puzzle days, and more '# FITB' on those days was associated with speedier solves for IS2. These properties provide some optimism that this feature will have some predictive value.*

**<h4>Figure 17. Scrabble Average**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/036437fe-d5b8-407b-a7c9-9ec80109910c)
*<h5>IS2 solve times and 'Scrabble Average' had a weak-to-nonexistent negative correlation on 15x15 puzzles (r= <-.01).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = -.04).<br>*

*'Scrabble Average' is another proprietary XWord Info measure, in which each letter in the answer grid is assigned its equivalent value in Scrabble. Since tile values in Scrabble increase with rarity of letter frequency in English texts, it would make sense that a higher value for this feature would be associated with *answers* of greater rarity. If anything, the opposite was true in practice here. Furthermore, as can be seen in the next series of figures, there are direct measures of answer rarity that *do* have strong positive correlations to solve times. So this one is a candidate to either be left out of predictive modeling entirely or to be combined with other answer rarity/difficulty measures to generate a useful predictive feature.*

**<h4>Figure 18. Number of Scrabble Illegal Answers**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/4e7e1388-27ac-4654-a286-3f701212a87a)
*<h5>IS2 solve times and '# Scrabble Illegal' had a weak positive correlation on 15x15 puzzles (r= .13).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = .19).<br>*

*'# Scrabble Illegal' answers is a proprietary measure of XWord Info that gets at answer rarity more directly than does 'Scrabble Average' (though not as directly as the measures in **Figs. 19 and 20**). Interestingly, the distributions for 15x15 puzzle days in the FDP were highly overlapping, other than a leftward shift for Monday that appears to account for the overall 15x15 puzzles (modest) positive correlation. With regard to Monday puzzles, it is notable that very low '# Scrabble Illegal' (<~20) seen essentially only on that day was associate with very fast solves. Monday aside, I had assumed prior to this analysis that the puzzle days with higher '# Open Squares' and 'Average Answer Length' would also have had proportionally more answers that were not standard English vocabulary words. A discernable trend for correlation strength within the more difficult puzzle days across the range of '# Scrabble Illegal' values was also lacking, with the possible exception of Saturday at the very high end of the feature distribution. Taken together, these findings suggest that more non-standard vocabulary *alone* may not strongly signify or predict puzzle difficulty.*  
 

**<h4>Figure 19. Number of Unique Answers**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/d64089bf-5cf0-4f6f-95f7-28f32797bb9b)
*<h5>IS2 solve times and '# Unique Answers' had a weak-to-moderate positive correlation on 15x15 puzzles (r= .31).<br>
GMS correlation strength on the same set of 15x15 puzzles was stronger (r = .38).<br>*

*<h5>A unique answer is defined here as one that does not appear in any other NYT crossword puzzle in either the Shortz or pre-Shortz eras (either before or after the puzzle release date). This is perhaps an overly stringent criterion to define answer rarity (see **Fig. 20** for a graded approach to defining answer rarity). Nonetheless the positive correlation was clearly apparent when considering all 15x15 puzzles together, consistent with the most difficult puzzle days (Fri and Sat) pulling most of the weight given their prominent rightward shifts in the FDP, and also within most of the individual puzzle days.*

**<h4>Figure 20. Freshness Factor**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/20a662ae-74e5-4cd8-a516-de5aafd56301)
*<h5>IS2 solve times and 'Freshness Factor' had a moderately strong positive correlation on 15x15 puzzles (r= .58).<br>
GMS correlation strength on the same set of 15x15 puzzles was considerably stronger, reaching the level of strong correlation (r = .67).<br>*

*<h5>'Freshness Factor' is yet another proprietary XWord Info measure that assesses the aggregate relative novelty of all answers in a given crossword puzzle as compared to those in all other crossword puzzles in the NYT archive. The much stronger correlation to IS2 solve times as compared to that for '# Unique Answers' suggests that there's much to be gained by taking a graded, as opposed to all-or-none, approach in assessing answer rarity.  More so than any other grid, clue or puzzle feature, 15x15 puzzle days peaked in this measure (seen in the FDP) in close concordance with the peaks in the per day sequence for solve times (see **Figs. 2 and 4**). The positive correlation was also seen to some degree within each of the individual puzzle days. This finding generates a prediction that, apart from recent puzzle day-specific solver performance prior to a given solve (see **Figure 22**), 'Freshness Factor' will be the most useful feature evaluated in this analysis for predictive modeling of solve performance.*


**<h4>Figure 21. Number of Wordplay Clues**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/f308807b-560b-4107-8ccd-e26898ad85d4)
*<h5>IS2 solve times and '# Wordplay Clues' had a moderate positive correlation on 15x15 puzzles (r= .33).<br>
GMS correlation strength on the same set of 15x15 puzzles was substantially stronger (r = .45).<br>*

*<h5>'# Wordplay' clues is an admittedly somewhat subjective measure that I have manually evaluated and calculated clue-by-clue across (nearly) the entire puzzle sample completed by IS2. The FDP for this feature has some interesting properties, including the clear result that later week (Thu, Fri, Sat) puzzles indeed have a larger allocation of 'trickier' clues than early week puzzles. There's also a prominent strong leftward shift for Monday puzzles. Taken together, these early and late week distribution offsets seem to account for the overall positive correlation cross 15x15 puzzles. However, it is potentialy interesting that the later week puzzle days (Thu-Sat) for this solver, unlike for the GMS or IS1, showed reverse sign (negative) correlations. This raises the possibility that this solver is unusually adept at wordplay-based clues in the difficult puzzle context. It will be interesting to see how this potential interaction with puzzle difficulty plays out in the preditive modeling phase.* 

**<h4>Figure 22. IS2 Adjusted Recent Performance**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/0fd48a14-5787-488d-9a40-33a7a470762a)
*<h5>IS2 raw solve times and 'IS2 Recent Performance Baseline (RPB)' had a strong positive correlation for 15x15 puzzles (r= .73).<br>
GMS raw solve times and 'GMS RPB' had a stronger correlation, reaching the level of very strong correlation (r = .84).<br>*

*<h5>The lowest puzzle day correlation for each of this solver (.27), IS1 (.14) and the GMS (.37) was for Thursday. This finding makes intuitive sense, as Thursday is arguably the most heterogenous puzzle day of all, with nearly every puzzle involving a gimmick of some sort (e.g., rebuses of various flavors). Friday and Saturday having relatively low correlations as compared to the early week puzzle days for all three solvers was also unsurprising given the relative heterogeneity these puzzles had across the range of puzzle features evaluated. There's also many more opportunities for a solver to get stuck for an extended period of time on a later week puzzle due to some particularly tricky clue(s) and/or quirks of puzzle geometry. One analysis I have not carried out yet, but would be interesting in the context of these findings, is if the size of the constructor pool covaries with correlation strength for RPB and performance on "new" puzzles.*

*<h5>Correlation Strength by Puzzle Day:*<br>
*IS2: Sun: .45, Mon: .46, Tue: .45, Wed: .44, Thu: .27, Fri: .30, Sat: .37*<br>
*GMS: Sun: .63, Mon: .55, Tue: .51, Wed: .45, Thu: .37, Fri: .40, Sat: .40*<br>
*GMS overall and by puzzle day correlations were taken from the entire GMS sample in the GMS-specific analysis*





# Supplementary Figures

**<h4>Figure S1. IS2 10-Puzzle Solve Time Moving Averages Adjusted by GMS Performance, by Puzzle Day** 

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/b94085ab-51c4-4457-9431-049c06a7d2f8)
*<h5>For each puzzle completed by IS2, % difference for the raw solve time from the global median solve time (GMST) was computed. The 10-puzzle moving average of this difference was then plotted, per puzzle day, by completion date. The volatility present in the raw solve times (see **Fig. 2 and Fig. 4**), including the upward spike in Q2-early Q3 2023, was still mostly present in these adjusted data plots, indicating that this volatility was due to factors other than by chance stretches of puzzles with substantially greater or lesser difficulty per puzzle day.*

**<h4>Supplementary Figure 2. Correlation Heatmapping of IS2 Individual Puzzle Performance vs Grid, Answer and Past Performance Features by Puzzle Day (15x15 Puzzle Days)**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/0b69a648-ae51-45d8-b789-cb429b903358)


**<h4>Supplementary Figure 3. Number of Rebus Squares vs IS2 Solve Time by Puzzle Day**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/f255007c-564b-4cd4-9de2-1da889f276f5)
*<h5>Only Thursday had an appreciable '# Rebus Squares' for IS2 solves. Rebus squares are those that must be filled with more than one letter, number or symbol for a given puzzle to be solved. There was a weak-to-moderate positive correlation for IS1 and a moderate one for GMS for Thursday, though a caveat is that the very large number of 0 rebus puzzles makes these correlations hard to interpret (ie, these are not exactly continuous distributions).*<br>

*Correlation Strength by Puzzle Day: IS2: Thu: .18; GMS: Thu: .27* 

**<h4>Supplementary Figure 4. Number of Circled Squares vs IS2 Solve Time by Puzzle Day**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/5e5cccb2-7e42-4dde-908c-fb4589fc1a32)
*<h5>Circled squares were virtually non-existent in the tougher (Fri and Sat) puzzles. The modest negative correlation seen across all 15x15 puzzle days (-.11) is attributable to the fact that most 15x15 puzzles with circles appeared early in the week. The smattering of puzzles with circles on Sunday almost all fell in the middle of the solve time range regardless of "# Circles", indicating that this feature didn't likely have a major impact on solve times.*

**<h4>Supplementary Figure 5. Number of Shaded Squares vs IS2 Solve Time by Puzzle Day**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/720ebb30-c21d-4d79-8436-07dbc9989c14)
*<h5>Shaded squares, like circled squares, were virtually non-existent in the tougher (Fri and Sat) puzzles. Also like with circled squares, their function is to reveal a puzzle theme and their presence may provide assistance to solvers on clues in which they are embedded. Most puzzles with shaded squares were within the bottom third of IS2 15x15 puzzle solve times, most likely due to shaded squares almost exclusively showing up only in early week puzzles. Also as with '# Circles', the smattering of Sunday puzzles almost all fell in the middle of the solve time range regardless of "# Shaded Squares", indicating that this feature also isn't likely having a major impact on solve times.* 










