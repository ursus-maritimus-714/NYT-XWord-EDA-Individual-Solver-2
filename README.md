# Exploratory Data Analysis of Individual Solver 2 (IS2) Performance on the New York Times Crossword Puzzle

## Introduction

### Project Overview
This summary reports on exploratory data analysis (EDA) of an individual solver's (Individual Solver 2; IS2) performance over a large subset of nearly 6 years (Mar. 2018 - Jan. 2024) of the [New York Times (NYT) crossword puzzle](https://www.nytimes.com/crosswords). Included are visual and statistical descriptions of trends in IS2 solve times across this period, performance relative to the 'Global Median Solver' (GMS; see next section), and the relationship between IS2 performance and a number of variables. These variables included properties of the puzzle grids (e.g., number of answers, number of black squares), clues and answers (e.g., frequency of wordplay in clues, aggregate rarity of answers in a puzzle), environment (e.g., time of day a puzzle was completed), constructor identity, and puzzle day-specific recent past performance prior to a given solve. This EDA led to identification of a set of features that hold promise as useful inputs to a predictive model of IS2 future performance.

Without access to two specific data sources this project would not have been possible. The first, [XWord Info: New York Times Crossword Answers and Insights](https://www.xwordinfo.com/), was my source for data on the puzzles themselves. This included a number of proprietary metrics pertaining to the grids, answers, clues and constructors. XWord Info has a contract with NYT for access to the raw data underlying these metrics, but I unfortunately do not. Therefore, I will not be able to share raw or processed data that I've acquired from their site. Nonetheless, [Jupyter notebooks](https://jupyter.org/) with all of my Python code for analysis and figure generation can be found [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/tree/main/notebooks)). The second, [XWStats](xwstats.com), was my source for historical solve time data for both IS2 and the GMS.

Similar analyses to those reported here for IS2 were performed on another individual's (IS2) data over a comparable sample size and timespan, and are summarized [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1?tab=readme-ov-file#readme).

### The Global Median Solver (GMS)

Many analyses included in this summary compare IS2 performance to that of the GMS over the set of all IS2 solves. My extensive summary analysis of GMS performance over a 6+ year timeframe (2018-2024) can be found [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Global-Median-Solver?tab=readme-ov-file#readme). XWStats (Matt) determines the global median solve time (GMST) for every individual puzzle from a pool of ~1-2K individual solvers of a given puzzle for whom he has (with their consent) acquired their data from NYT. Though Matt adopted the term "global" to describe this solver sample per-puzzle, it likely skews faster than the overall population of solvers. The reasons for this assumption are twofold; only solvers who actually complete a given puzzle are included in its sample, and each sample contains only solvers motivated enough by the prospect of improvement to track their own progress to begin with. 

GMSTs improved over the complete set of puzzles (N=2,212) issued between January 1, 2018 and January 21, 2024 (**Figure 1**), with fairly dramatic improvement seen early on for some puzzle days and graded improvement continuing for each puzzle day until the end of the sample period (top panel). The 2-year interval density plots of raw solve time distributions (bottom panels) show that performance on individual puzzle days became more consistent over time (higher peaks with narrower distributions). Because I did not have access to the raw solver data from which the GMSTs were drawn, however, it was not possible to disentangle improvement for individual "early adopters" of Matt's tracking software versus stronger solvers joining the solver pool over time. Note also that GMS performance is tracked in my analyses by puzzle issue date, as I did not have access to GMS puzzle completion dates. It's reasonably safe to assume, however, that the GMS (a different individual solver for most puzzles, presumably) solved in approximately the sequence of puzzle issue. IS2 performance, in contrast, is tracked by puzzle completion data since I *was* able to obtain completion timestamps for this solver's completed puzzles with Matt's assistance.  

**Figure 1. GMS Solve Time Overview by Puzzle Day: 10-Puzzle Moving Averages and Distributions of Raw Values**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/87e7395f-282d-4e60-9402-ad28d0860d10)
*<h5>GMS Final (as of Jan. 21, 2024) 10-puzzle moving average of solve time (m), per puzzle day:*<br>
*Sun: 28.7, Mon: 5.7, Tue: 7.8, Wed: 12.0, Thu: 15.6, Fri: 17.8, Sat: 21.0*<br>


## Results
### Individual Solver 2 (IS2) Performance Over Time

IS2 solved N = 1,053 puzzles in the sample period: 89 (8.5%) in 2018, 9 in 2019 (.8%), 282 in 2020 (26.8%), 28 (2.7%) in 2021, 79 (7.5%) in 2022, and 566 (53.8%) in 2023/24 (through Jan. 16, 2024). The total solve time for IS2 was 16.9 days (2018: 2.2 days; 2019: .14 days; 2020: 5.1 days; 2021: .25 days; 2022: .97 days; 2023/24: 8.3 days). The total solve time for the GMS over this same set of puzzles was 14.0 days. 

IS2's per-puzzle day 10-puzzle moving averages across the sample period are shown in **Figure 2** (top panel). The first 5 years were characterized by long periods of little solve activity (flat stretches in lines) punctuated by rapid and dramatic improvements across puzzle days during months-long bursts of activity. There was a short-term, spiked increase in solve times across puzzles days when solving resumed after a long layoff in Q2 2023. Then, from late Q3 2023 through the end of the sample period, IS2 showed dramatic improvement across puzzle days relative to even pre-spike baselines. **Supplementary Figure 1** shows that the volatility of IS2's per-puzzle day solve times in 2023 was *not* likely due to chance stretches of puzzles with higher or lower than usual median difficulty (as determined by GMS performance on the same puzzle set). Improvement over the last ~4 months of the sample period was especially apparent on the more difficult puzzle days (Thu-Sun). Leftward shifts of peaks and reduced bimodality of by-day solve time distributions in the 2023/2024 density plot (**Fig. 2**, bottom right) also demonstrate this recent improvement in solve form. 

**Figure 2. Solve Time Overview by Puzzle Day: 10-Puzzle Moving Averages and Distributions of Raw Values**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/1b5bccbe-eaf1-445c-abdd-ac72bf20b7cc)
*<h5>IS2 Final (wk of Jan. 15, 2024) 10-puzzle moving average of solve time (m), per puzzle day:*<br>
*Sun: 26.8, Mon: 4.7, Tue: 7.1, Wed: 9.6, Thu: 19.4, Fri: 17.6, Sat: 22.2*<br>


###
**Figure 3** shows IS2's solve time performance trajectory in violin plots with swarm plot overlays, broken out by 2-3 year solve date intervals. These representations may be somewhat easier to digest than the line plots in **Fig. 2**, as they remove the compressing effect of the long intervals with minimal solve activity. They also have the advantage of providing a clear visual sense of the number of solves and distribution shape, per interval. Violin plots show both the range (vertical extent) and distribution characteristics (width as it varies across the y-axis range) for each puzzle day, per solve interval. Black lines on the violin plot demarcate solve time quartiles per puzzle day. Swarm plot overlays per puzzle day show individual puzzle raw solve times.   

**Figure 3. Solve Time Overview by Puzzle Day: Violin Plots With Swarm Plot Overlay**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/edd0c4e9-3662-489a-bc85-21b57c1c05f5)
*<h5>Median[IQR] solve time (m), per puzzle day, per solve interval:*<br>
*2018/19: Sun: 69.3[59.4-82.2], Mon: 10.3[8.7-11.8], Tue: 15.4[11.2-24.5], Wed: 21.5[14.9-34.2], Thu: 43.4[39.6-63.8], Fri: 33.3[30.7-48.5], Sat: 52.0[41.7-55.7]*<br>
*2020-22: Sun: 43.0[36.6-52.4], Mon: 7.1[5.9-8.2], Tue: 10.6[8.7-12.6], Wed: 14.0[11.5-20.0], Thu: 25.0[18.2-31.0], Fri: 26.3[18.4-32.0], Sat: 34.8[28.0-50.4]*<br>
*2023/24: Sun: 32.3[26.5-40.9], Mon: 5.7[4.8-6.5], Tue: 7.4[6.8-8.5],   Wed: 11.8[9.9-14.3], Thu: 19.8[15.8-26.0], Fri: 19.1[14.8-25.0], Sat: 26.2[20.5-36.5]*<br>

###
Because over half of IS2' total solves (n=566) came in 2023-2024, and there was such rapid and dramatic improvement over the latter ~1/3 of that time range, zoom-in and 2-interval partition of this time range is depicted below in **Figure 4**. IS2 had n=319 solves in the final 3.5 months of the time range, spread roughly equivalently across puzzle days. The dramatically improved solve performance (Sat median solve time, for ex., dropped from 38.5 to 23.5 minutes) during this period was likely driven by the large amount of solving in a condensed period of time.    

**Figure 4. Solve Performance in 2023-2024**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/0819c707-6096-4e9f-ad8a-4a5364e19f1c)
*<h5>Median[IQR] solve time (m), per puzzle day, per solve interval:*<br>
*Apr 2023-Sept 2023: Sun: 41.2[32.6-47.1], Mon: 5.9[5.5-6.7], Tue: 7.7[6.9-8.9], Wed: 13.2[10.6-14.9], Thu: 26.4[18.9-32.1], Fri: 24.2[18.0-32.0], Sat: 38.5[26.7-46.1]*<br>
*Oct 2023-Jan 2024:  Sun: 28.3[23.6-34.2], Mon: 5.3[4.7-6.2], Tue: 7.3[6.6-8.3], Wed: 10.2[8.5-12.4], Thu: 17.0[14.2-20.8], Fri: 17.7[13.0-23.2], Sat: 23.5[17.5-32.5]*<br>



### Individual Solver 2 (IS2) Performance Vs Global Median Solver (GMS) 

The next series of figures directly compare IS2 solve performance to that of the GMS over the same puzzle set. For these analyses, IS2 solves were broken into 2 solve intervals: pre-2023 (n=487; 46.2% of total solves; 2023/24: n=566; 53.8%). Per puzzle day, in the figures relevant to these analyses, pre-2023 solves are represented by lighter-colored points and regression lines and 2023/24 solves by darker-colored ones. 

**Figure 5** shows per-puzzle day scatterplots of GMS (x-axis) versus IS2 (y-axis) raw solve times. Points falling on the dashed diagonal line represent identical raw solve times for IS2 and GMST on a given puzzle, points above and below this line represent "wins" for the GMS and IS2, respectively. IS2 win % across all puzzle days improved greatly from the pre-2023 (28.7%) to 2023/24 interval (49.2%). Win %s for IS2 also increased dramatically for most puzzle days in 2023/24, including a >2x increase for both Tuesday (34.6% to 71.2%) and Saturday (13.7% to 29.8%). The lowest IS2 win % for both time intervals was for Saturday, and Monday yielded the highest and second highest IS2 win %s in the pre-2023 and 2023/24 intervals, respectively. The per puzzle day regression lines show that there was a relatively high degree of correlation in raw solve times between IS1 and GMST (range across puzzle days and solve intervals: .55-.82). The downward shifts in all puzzle day regression lines between the older and more recent solve intervals also indicate improved performance relative to the GMS. However, a caveat in interpretation here is that IS2 solved many older puzzles in 2023-2024, so the GMS was earlier on "their" own improvement curve when solving the same puzzles. The next figure will remove this issue by examining the IS2-GMS solve time relationship on data normalized to each solver's respective recent day-specific performance prior to a given solve (calculated with respect to completion date for IS2 and issue date for GMS). 

**Figure 5. IS2 vs GMS: Comparison of Raw Solve Performance by Puzzle Day and Solve Interval**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/69206704-4ea9-4efb-b54c-5657e49ab57b)
*<h5> Win % for IS2 vs GMS, by IS2 solve interval:*<br>
*pre-2023: All: 28.7, Sun: 24.2, Mon: 48.1, Tue: 34.6, Wed: 29.1, Thu: 20.8, Fri: 22.2, Sat: 13.7*<br>
*2023/24:  All: 49.3, Sun: 48.2, Mon: 65.7, Tue: 71.8, Wed: 57.5, Thu: 40.2, Fri: 41.9, Sat: 29.8*<br>

*<h5> Mean(stdev) Solve Time Difference (m) for IS2 vs GMS, by IS2 solve interval (negative denotes faster for IS2):*<br>
*pre-2023: All: 6.1(10.5), Sun: 9.6(13.6), Mon: .64(2.3), Tue: 1.8(3.4), Wed: 3.4(6.1), Thu: 8.7(11.1), Fri: 7.9(11.8), Sat: 15.3(14.8)*<br>
*2023/24:  All: 2.4(8.1), Sun: 1.4(8.6), Mon: -.13(1.2), Tue: -.65(1.2), Wed: -.08(3.3), Thu: 3.0(7.0), Fri: 3.3(8.6), Sat: 7.8(12.7)*<br>

###
Along with comparison of raw solve performance between IS2 and GMS, the degree to which the same puzzles were *relatively* difficult for the two solvers was addressed. Per solver (IS2 or GMS) each raw solve time was taken as a % difference from a decay-time weighted average of the *previous* 10 puzzles solved on the same puzzle day ('Recent Performance Baseline'; RPB). These RPB-adjusted solve times were then plotted against each other on a per puzzle day and per solve period basis (**Figure 6**). Points falling in the lower left ("relatively easy for both solvers") and upper right ("relatively hard for both solvers") quadrants represent concordance of relative difficulty for a given puzzle. The most common outcome across puzzle days for both solve periods was "relatively easy for both solvers" (pre-2023: 44%; 2023/24: 41%), and the second most common was "relatively hard for both solvers" (pre-2023: 26.7%; 2023/24: 29.3%). It's not surprising that "easy" concordance was more common than "hard" concordance, since solvers constantly improved/outperformed their RPB. A substantial minority (~30%) of puzzles, however, were either relatively easy for IS2 and relatively hard for GMS or vice versa (lower right and upper left quadrants, respectively). This suggests that environmental and puzzle-specific variables may affect different solvers in different ways. Starting in the next section, the focus will be on summarizing the effects of some of these variables on IS2 (and GMS) performance.  

**Figure 6. IS2 vs GMS: Comparison of Baseline-Adjusted Solve Performance by Puzzle Day and Solve Interval**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/fc1b5217-855c-456a-b368-4392fe801a51)
*<h5>Overall, correlations between baseline-normalized IS2 and GMS solve times were moderately-to-strongly positive, with greater strength for most puzzle days in the more recent solve interval.*<br>
*IS1-GMS Correlation (Pearson r) of recent performance baseline (RPB)-adjusted solve difficulty by IS2 solve interval:*<br>
*pre-2023: All: .66, Sun: .69, Mon: .49, Tue: .73, Wed: .67, Thu: .71, Fri: .53, Sat: .75*<br>
*2023/24:  All: .58, Sun: .65, Mon: .53, Tue: .71, Wed: .5, Thu: .68, Fri: .52, Sat: .55*<br>

*<h5> IS2-GMS Quadrant Percentage by IS2 solve interval: Lower Left(LL)/Upper Right(UR)/Upper Left(UL)/Lower Right(LR)*<br>
*LL: Relatively Easy for Both IS2 & GMS/ UR: Hard for IS2 & GMS/ UL: Easy for GMS-Hard for IS2/ LR: Easy for IS2-Hard for GMS*<br> 
*pre-2023: All: 44.0/26.7/12.5/16.9, Sun: 44.3/26.2/13.1/16.4, Mon: 39.7/28.2/7.7/24.4, Tue: 41.3/30.0/13.8/15.0, Wed: 42.3/28.2/10.3/19.2, Thu: 45.1/26.8/14.1/14.1, Fri: 46.8/22.6/17.7/12.9,<br> Sat: 52.0/22.0/12.0/14.0*<br>
*2023/24:  All: 41.0/29.3/12.0/17.7, Sun: 43.4/30.1/9.6/16.7, Mon: 38.6/22.9/14.3/24.3, Tue: 47.9/29.6/11.3/11.3, Wed: 38.4/27.4/11.0/23.3, Thu: 41.5/32.9/9.8/15.9, Fri: 39.8/29.0/17.2/14.0,<br> Sat: 38.3/32.0/10.6/19.1*<br>

### IS2 Performance by Puzzle Constructor(s)

A high proportion of puzzles solved by IS2 (70%) were authored by either repeat individual constructors or specific constructor teams (both referred to as "constructor" from here forward). This afforded the opportunity to evaluate which constructors IS2 tended, in a relative sense, to struggle or do well against. Per constructor, the mean of % difference from puzzle day-specific recent performance baseline (RPB; see text section pertaining to **Fig. 6**) was computed. This measure allowed assessment of constructor difficulty adjusted for solver form at the time of a given solve and constructor past puzzle day heterogeneity. **Figure 7** shows heatmapping of IS2 performance, using this normalized measure, against the n=63 constructors contributing >=4 puzzles over the sample period. While only 13% of constructors contributed this many puzzles, this group contributed 41% of all puzzles solved. **Fig. 7** also shows this metric for the GMS on the same set of puzzles for the sake of qualitative comparison. Warmer colors (-%) indicate that the solver solved relatively fast against a given constructor; cooler colors (+%) indicate the opposite. "Hot" or "cold" constructors for IS2 tended to also be relatively fast or slow, respectively, for GMS as well. However, there was clearly a substantial degree of discordance in terms of specific order and some constructors stood out as being either "hot" for IS2 but "cold" for the GMS (e.g., Adrian Johnson, Drew Schmenner) or vice versa (e.g., Rafael Musa, Will Nediger). 

**Figure 7. Heatmapping of IS2 and GMS Performance Against Individual Constructors**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/9dc030ce-e5e8-4f83-95fa-b9f01a404928)

The next correlational analysis was aimed at assessing the potential predictive value of IS2's baseline-adjusted past performance against specific constructors on their future performance against the same constructor. **Figure 8** shows this correlation between IS2 baseline-adjusted performance (as mean % difference from RPB) against a given constructor (x-axis) and performance on the next solved individual puzzle by that constructor (y-axis). This analysis was restricted to only the n=228 puzzles by the constructor included in **Fig. 7** that were solved *after* >=3 previous puzzles by the same constructor (based on puzzle completion date for IS2, but issue date for GMS). There was a moderate positive correlation for IS2, but a substantially stronger one for GMS. It may make sense for the 'typical' solver to have a more reliable relationship with a specific constructor than an individual solver, though predictive modeling will say a lot more on this topic.  

**Figure 8. IS2 and GMS: Past Performance Against Individual Constructors as "Prediction" of Next Puzzle Performance Against the Same Constructor**  

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/12283951-36f5-4344-8d1a-e38b090e410d)
<h5>Pearson correlation coefficient (r): IS2: .23, GMS: .32

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
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/74c04f3d-5884-4f58-97f4-721c62888adc)
*<h5>IS2 solve times and '# Open Squares' had a moderately strong positive correlation on 15x15 puzzles (r= .49).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = .56).<br>*

*'# Open Squares' is a proprietary measure from XWord Info that counts all white squares that are *not* bordered by black squares. '# Open Squares' was strongly positively correlated to 'Average Answer Length' (see matrices above), so it makes sense that more open squares was also positively correlated with solve times. The IS2 FDP shows that the most difficult puzzle days (Fri and Sat) had a rightward shift in '# Open Squares' relative to the easier 15x15 puzzle days. A large amount of the overall 15x15 correlation for IS2 appears to be accounted for by these more difficult puzzles with large numbers (>~80) of open squares.* 

**<h4>Figure 13. Number of Black Squares**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/547bbd06-6a72-4fcf-94f0-d118d83c9b4a)
*<h5>IS2 solve times and '# Black Squares' had a weak-to-moderate negative correlation on 15x15 puzzles (r= -.34).<br>
GMS correlation strength on the same set of 15x15 puzzles was stronger, reaching the level of moderate correlation (r = -.40).<br>*

*This relationship was essentially the opposite (albeit a weaker form) of that between solve times and '# Open Squares' (more black squares = shorter answers = easier answers). For IS2, this correlation was consistently apparent across all puzzle days, though with variable strength. The correlation was relatively strong for both Friday and Saturday, which are strongly shifted to the left of the other 15x15 puzzle days in the FDP.*

**<h4>Figure 14. Average Answer Length**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/a4599665-175f-4286-bd27-47e01b98475e)
*<h5>IS2 solve times and 'Average Answer Length' had a moderately strong positive correlation on 15x15 puzzles (r= .55).<br>
GMS correlation strength on the same set of 15x15 puzzles was considerably stronger, reaching the level of strong correlation (r = .66).<br>*

*This finding was consistent with other grid feature relationships to IS2 solve times, which makes sense since longer answers meant more multiword and relatively-rare answers (see correlation matrices above and **Figs. 18-20**). This correlation was apparent within most of the individual puzzle days, and was stronger for later week days, as was typical for grid features. As with '# Answers' Monday stood alone among puzzle days in showing the reverse correlation sign. Given that these two features are themselves strongly negatively correlated (see **Fig. 10**), it makes sense that Monday would again serve as the exception that proves the rule. Longer answers that are still easy may increase solver speed in the aggregate by reducing the amount of clues consumed needed for a solve, without a counterbalancing 'difficulty penalty' that might occur with longer answers on later puzzle days.* 

*It is also noteworthy that the peaks in the FDP (per-15x15 puzzle day) are well separated and track in the same sequence as the peaks in solver performance per-puzzle day (see **Figs. 2 and 4**). The strong correlation level, FDP peak separation, and alignment with the per-puzzle day solve time sequence (perhaps excepting Thu-Fri) raises the possibility that this feature will be particularly useful in predictive modeling.*

**<h4>Figure 15. Number of Cheater Squares**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/e0812ac7-ce66-4474-8bd9-fca5fd31ae8a)
*<h5>IS2 solve times and '# Cheater Squares' had a weak positive correlation on 15x15 puzzles (r= .11).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = .18).<br>*

*Cheater Squares are black squares than can be removed without affecting the overall word count of the grid. These squares make construction easier (hence their name), and it can be seen in the FDP that large numbers of them (say, >10) almost always appeared on the difficult puzzle days. Within each puzzle day, it's clear that puzzles with larger numbers of these squares tended to be easier for IS2 (also true for IS1 and the GMS). So the seeming paradox between the overall 15x15 trend and the individual puzzle day trends is likely related to the competing effects on solve times of an increase in '# Cheater Squares' allowing trickier constructions, but also simultaneously reducing '# Answers' and 'Average Answer Length'. Incidentally, the reason cheater squares were only rarely seen in odd numbers is the NYT general requirement for grid symmetry.*

#### *Answer and Clue Content Features*
**<h4>Figure 16. Number of Fill-in-the-Blank Answers**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/eb4e542a-4790-417e-a129-cd888f787e2d)
*<h5>IS2 solve times and '# Fill-in-the-Blank Answers' had a weak-to-moderate negative correlation on 15x15 puzzles (r= -.25).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = -.26).<br>*

*Taken together, the FDP and scatterplots indicate that most of the strength of this correlation was due to the easiest puzzles (note the rightward FDP peak shift for Mon, even relative to Tue) employing a heavy dose of FITB answers. It's also noteworthy that the most difficult puzzle days (Thu and Fri) clearly made less use of FITB answers than the other puzzle days. It will be interesting to see how important this feature is in the modeling phase to prediction of early week solve times, specifically.*

**<h4>Figure 17. Scrabble Average**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/100f601c-21b6-4d50-8d7a-8d043e665c5e)
*<h5>IS2 solve times and 'Scrabble Average' had a weak-to-nonexistent negative correlation on 15x15 puzzles (r= -.01).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = -.03).<br>*

*'Scrabble Average' is another proprietary XWord Info measure, in which each letter in the answer grid is assigned its equivalent value in Scrabble. Since tile values in Scrabble increase with rarity of letter frequency in English texts, it would make sense that a higher value for this feature would be associated with *answers* of greater rarity. If anything, the opposite was true in practice here. Furthermore, as can be seen in the next series of figures, there are direct measures of answer rarity that *do* have strong positive correlations to solve times. So this one is a candidate to either be left out of predictive modeling entirely or to be combined with other answer rarity/difficulty measures to generate a useful predictive feature.*

**<h4>Figure 18. Number of Scrabble Illegal Answers**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/dbd5acfc-bb9a-45a9-a037-0a00e29a1c78)
*<h5>IS2 solve times and '# Scrabble Illegal' had a weak positive correlation on 15x15 puzzles (r= .15).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = .20).<br>*

*'# Scrabble Illegal' answers is a proprietary measure of XWord Info that gets at answer rarity more directly than does 'Scrabble Average' (though not as directly as the measures in **Figs. 19 and 20**). Interestingly, this (modest) positive correlation was seen both across all 15x15 puzzles and within each puzzle day (save for Fri). Also interesting is that, apart from a Monday relative leftward shift in the FDP, the distributions for the other 15x15 puzzle days were highly overlapping. I had assumed that the days with more open squares and longer average answers would also have substantially more answers that are not standard English vocabulary words. This finding suggests that more non-standard vocabulary *alone* may not signify or predict puzzle difficulty.*  

**<h4>Figure 19. Number of Unique Answers**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/8d5c1554-0d83-4200-a59d-c1cec831d3f9)
*<h5>IS2 solve times and '# Unique Answers' had a weak-to-moderate positive correlation on 15x15 puzzles (r= .29).<br>
GMS correlation strength on the same set of 15x15 puzzles was stronger (r = .38).<br>*

*<h5>A unique answer is defined here as one that does not appear in any other NYT crossword puzzle in either the Shortz or pre-Shortz eras (either before or after the puzzle release date). This is perhaps an overly stringent criterion to define answer rarity (see **Fig. 20** for a graded approach to defining answer rarity). Nonetheless, the positive correlation was clearly apparent when considering all 15x15 puzzles together and also especially within the most challenging puzzle day (Sat). It is also clear in the FDP that '# Unique Answers' tended to increase as puzzle day difficulty increased.*

**<h4>Figure 20. Freshness Factor**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/9f4d4936-76b0-4b35-8d34-e9ad453da855)
*<h5>IS2 solve times and 'Freshness Factor' had a moderately strong positive correlation on 15x15 puzzles (r= .56).<br>
GMS correlation strength on the same set of 15x15 puzzles was considerably stronger, reaching the level of strong correlation (r = .66).<br>*

*<h5>'Freshness Factor' is yet another proprietary XWord Info measure that assesses the aggregate relative novelty of all answers in a given crossword puzzle as compared to those in all other crossword puzzles in the NYT archive. The much stronger correlation to IS2 solve times as compared to that for '# Unique Answers' suggests that there's much to be gained by taking a graded, as opposed to all-or-none, approach in assessing answer rarity.  More so than any other grid, clue or puzzle feature, 15x15 puzzle days peaked in this measure (seen in the FDP) in close concordance with the peaks in the per day sequence for solve times (see **Figs. 2 and 4**). This finding generates a prediction that, apart from recent puzzle day-specific solver performance prior to a given solve (see **Figure 22**), 'Freshness Factor' will be the most useful feature evaluated in this analysis for predictive modeling of solve performance.*


**<h4>Figure 21. Number of Wordplay Clues**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/c56989c7-c953-4794-891c-5a2c85ccf03f)

*<h5>IS2 solve times and '# Wordplay Clues' had a moderate positive correlation on 15x15 puzzles (r= .32).<br>
GMS correlation strength on the same set of 15x15 puzzles was substantially stronger (r = .44).<br>*

*<h5>'# Wordplay' clues is an admittedly somewhat subjective measure that I have manually evaluated and calculated clue-by-clue across (most of) the entire puzzle sample completed by IS2. It's clear in the FDP that the later week 15x15 puzzles in the sample employed substantially more 'Wordplay' than the early week puzzles. This relationship to difficulty by puzzle day accounts for the overall moderate positive correlation across all 15x15 puzzles. The negative correlation with later day solve times, particularly Friday, is interesting. Perhaps IS2 is especially adept at decoding tricky wordplay, as this reversal of the overall 15x15 correlation was not seen for either IS1 or the GMS. As a final note, the apparent strong Monday positive correlation was due to slow solve times on the extremely rare smattering of puzzles for that day with >2-3 wordplay clues.* 

**<h4>Figure 22. IS2 Adjusted Recent Performance**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/52745839-1ecc-4c75-80cd-3a62bb8c221d)
*<h5>IS2 solve times and 'IS2 Adjusted Recent Performance' had a strong positive correlation on 15x15 puzzles (r= .74).<br>
GMS solve time and 'GMS Adjusted Recent Performance' had correlation strength on the same set of 15x15 puzzles that was stronger, reaching the level of very strong correlation (r = .85).<br>*

*<h5>To obtain this measure for a given puzzle, a solver's (either IS2 or GMS) 10 most recent *prior* puzzles from the same puzzle day were averaged after first being decay weighted (10 for the most recent prior puzzle, 9 for the one before that and so on down to a weight of 1 for the 10th prior puzzle). Recent past performance across all 15x15 puzzles for IS2 (and, to an even larger degree, for GMS) by this measure was more strongly correlated to performance on the "next" puzzle than were the specific characteristics of that puzzle.*

*<h5>Correlation strengths for the early week 15x15 days (Mon-Wed) were higher than those for the later week days, and this was also true in the analyses for IS1 and the GMS. This trend likely is related to the relative heterogeneity of later week puzzles, both in terms of tricks/gimmicks employed and also in general difficulty. The lowest puzzle day correlation for both the GMS and IS1 was for Thursday, arguably the most heterogenous puzzle day of all as there's almost always a gimmick involved (e.g., rebuses of various flavors). Interestingly, Friday and Saturday both had substantially lower correlations for IS2 than did Thursday. This is another indication that optimally modeling individual solver performance, as compared to modeling the 'typical' solver, will be a somewhat bespoke task.*

*<h5>Correlation Strength by Puzzle Day:*<br>
*IS2: Sun: .58, Mon: .60, Tue: .60, Wed: .58, Thu: .50, Fri: .35, Sat: .39*<br>
*GMS: Sun: .62, Mon: .54, Tue: .51, Wed: .44, Thu: .37, Fri: .40, Sat: .39*<br>
*These GMS by-puzzle day correlations are taken from the entire GMS sample in the GMS-specific analysis*





# Supplementary Figures

**<h4>Supplementary Figure 1. IS2 10-Puzzle Solve Time Moving Averages Adjusted by GMS Performance, by Puzzle Day** 

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/99d0ebad-e6f9-4044-bdd4-111239ea9ab8)
*<h5>For each puzzle completed by IS2, % difference for the raw solve time from the global median solve time (GMST) was computed. The 10-puzzle moving average of this difference was then plotted, per puzzle day, by completion date. The volatility present in the raw solve times (see **Fig. 2**), including the upward spike in Q2-early Q3 2023, was still mostly present in these adjusted data plots, indicating that this volatility was due to factors other than by chance stretches of puzzles with substantially greater or lesser difficulty per puzzle day.*

**<h4>Supplementary Figure 2. Correlation Heatmapping of IS2 Individual Puzzle Performance vs Grid, Answer and Past Performance Features by Puzzle Day (15x15 Puzzle Days)**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/0b69a648-ae51-45d8-b789-cb429b903358)


**<h4>Supplementary Figure 3. Number of Rebus Squares vs IS2 Solve Time by Puzzle Day**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/1be473f6-3fba-435e-a6ba-0945ec487d08)
*<h5>Rebus Squares are squares that must be filled with more than one letter, number or symbol for a given puzzle to be solved. Only Thursday had an appreciable '# Rebus Squares' in the IS2-completed puzzle sample (IS1 solved more Sunday puzzles with Rebuses), and there was a weak positive correlation between '# Rebus Squares' for this puzzle day for both IS2 and the GMS. A caveat here is that the very large number of 0 rebus puzzles makes these correlations hard to interpret (ie, these are not exactly continuous distributions).*<br>

*Correlation Strength by Puzzle Day: IS2: Thu: .11; GMS: Thu: .19* 

**<h4>Supplementary Figure 4. Number of Circled Squares vs IS2 Solve Time by Puzzle Day**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/1d87cc42-b84e-44dc-bb3a-4d673fb03828)
*<h5>Circled squares were virtually non-existent in the tougher (Fri and Sat) puzzles. Their function is to reveal a puzzle theme, and in theory a solver can use this knowledge to "back in" to some full answers. Despite the apparent negative correlation for all 15x15 puzzles, the puzzle days with considerable '# Circles' mostly showed weakly positive correlations. One could speculate here, but it's probably not worth the effort; but there's potential for a small enhancement to modeling on a day-specific basis.*

**<h4>Supplementary Figure 5. Number of Shaded Squares vs IS2 Solve Time by Puzzle Day**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/558d4c7f-2c18-4aa9-8bc7-aa6e66c082cb)
*<h5>Shaded squares, like circled squares, were virtually non-existent in the tougher (Fri and Sat) puzzles. Also similarly to circled squares, their function is to reveal a puzzle theme and their presence may provide assistance to solvers on clues in which they are embedded. Though most puzzles with shaded squares were within the bottom third of IS2 15x15 puzzle solve times, this was likely mostly due to the fact that they essentially only occurred in early week puzzles. As with circles, it can't hurt to include his feature in first-pass modeling and there might be some puzzle day-specific accuracy improvements with its inclusion.* 









