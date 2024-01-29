
# Exploratory Data Analysis of Individual Solver 2 (IS2) Performance on the New York Times Crossword Puzzle

## Introduction

### Project Overview
This summary reports on exploratory data analysis (EDA) of an individual solver's (Individual Solver 2; IS2) performance over a large subset of nearly 6 years (Mar. 2018 - Jan. 2024) of the [New York Times (NYT) crossword puzzle](https://www.nytimes.com/crosswords). Included are visual and statistical descriptions of trends in IS2 solve times across this period, performance relative to the 'Global Median Solver' (GMS; see next section), and the relationship between IS2 performance and a number of variables. These variables included properties of the puzzle grids (e.g., number of answers, number of black squares), clues and answers (e.g., frequency of wordplay in clues, aggregate rarity of answers in a puzzle), environment (e.g., time of day a puzzle was completed), constructor identity, and puzzle day-specific recent past performance prior to a given solve. This EDA led to identification of a set of features that hold promise as useful inputs to a predictive model of IS2 future performance.

Without access to two specific data sources this project would not have been possible. The first, [XWord Info: New York Times Crossword Answers and Insights](https://www.xwordinfo.com/), was my source for data on the puzzles themselves. This included a number of proprietary metrics pertaining to the grids, answers, clues and constructors. XWord Info has a contract with NYT for access to the raw data underlying these metrics, but I unfortunately do not. Therefore, I will not be able to share raw or processed data that I've acquired from their site. Nonetheless, [Jupyter notebooks](https://jupyter.org/) with all of my Python code for analysis and figure generation can be found [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/tree/main/notebooks)). The second, [XWStats](xwstats.com), was my source for historical solve time data for both IS2 and the GMS.

Similar analyses to those reported here for IS2 were performed on another individual's (IS2) data over a comparable sample size and timespan, and are summarized [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1?tab=readme-ov-file#readme).

### The Global Median Solver (GMS)

Many analyses included in this summary compare IS2 performance to that of the GMS over the set of all IS2 solves. My extensive summary analysis of GMS performance over a 6+ year timeframe (2018-2024) can be found [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Global-Median-Solver?tab=readme-ov-file#readme). XWStats (Matt) determines the global median solve time (GMST) for every individual puzzle from a pool of ~1-2K individual solvers from whom he has (with their consent) acquired personal solve data. Though Matt adopted the term "global" to describe this solver sample per-puzzle, it likely skews faster than the overall population of solvers. The reasons for this assumption are twofold; only solvers who actually complete a given puzzle are included in its sample, and each sample contains only solvers motivated enough by the prospect of improvement to track their own progress to begin with. 

GMSTs improved on each puzzle day over the complete set of puzzles (N=2,218) issued between January 1, 2018 and January 27, 2024 (**Figure 1**). This improvement was fairly dramatic in the first few years for some puzzle days (most prominently for Sun), and graded improvement continued for each puzzle day until the end of the sample period (top panel). The 2-year interval density plots of raw solve time distributions (bottom panels) show that performance on individual puzzle days became more consistent over time (higher peaks with narrower distributions). Because I did not have access to the raw solver data from which the GMSTs were drawn, however, it was not possible to disentangle improvement and increased consistency for individual "early adopters" of Matt's tracking software versus stronger solvers joining the solver pool over time. Note also that GMS performance was tracked in my analyses by puzzle issue date, as I did not have access to GMS puzzle completion dates. It's reasonably safe to assume, however, that the GMS (a different individual solver for most puzzles, presumably) solved in approximately the sequence of puzzle issue. IS2 performance, in contrast, was tracked by puzzle completion data since I *was* able to obtain completion timestamps for my own solves with Matt's assistance.  

**Figure 1. GMS Solve Time Overview by Puzzle Day: 10-Puzzle Moving Averages and Distributions of Raw Values**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/b1f6464c-b57f-402b-a2b7-8f44716f2350)
*<h5>GMS Final (as of Jan. 27, 2024) 10-puzzle moving average of solve time (m), per puzzle day:*<br>
*Sun: 28.8, Mon: 5.7, Tue: 7.7, Wed: 11.4, Thu: 15.2, Fri: 17.3, Sat: 21.2*<br>



## Results
### Individual Solver 2 (IS2) Performance Over Time

IS2 solved N = 1,071 puzzles in the sample period: 89 (8.3%) in 2018, 9 in 2019 (.8%), 282 in 2020 (26.3%), 28 (2.6%) in 2021, 79 (7.4%) in 2022, and 584 (54.5%) in 2023/24 (through Jan. 28, 2024). The total solve time for IS2 was 17.1 days (2018: 2.2 days; 2019: .14 days; 2020: 5.1 days; 2021: .25 days; 2022: .97 days; 2023/24: 8.4 days). The total solve time for the GMS over this same set of puzzles was 14.2 days. 

IS2's per puzzle day 10-puzzle moving averages across the sample period are shown in **Figure 2** (top panel). The first 5 years were characterized by long periods of little solve activity (flat stretches in lines) punctuated by rapid and dramatic improvements across puzzle days during months-long bursts of activity. There was a short-term, spiked increase in solve times across puzzles days when solving resumed in Q2 2023 after a long layoff. Then, from late Q3 2023 through the end of the sample period, IS2 showed dramatic improvement across puzzle days relative to even pre-spike baselines. **Supplementary Figure 1** shows that the volatility of IS2's per puzzle day solve times in 2023 was *not* likely due to chance stretches of puzzles with higher or lower than usual median difficulty (as determined by GMS performance on the same puzzle set). Improvement over the last ~4 months of the sample period was especially apparent on the more difficult puzzle days (Thu-Sun). The leftward shift in peaks for the by day solve time distributions in the 2023/2024 density plot (**Fig. 2**, bottom right) clearly demonstrates this recent improvement in solve form. Additionally, overall distribution widths narrowed considerably across solve intervals for early week (Mon-Wed) puzzle days. This indicates increased consistency of solve performance over time for IS2.    

**Figure 2. Solve Time Overview by Puzzle Day: 10-Puzzle Moving Averages and Distributions of Raw Values**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/f30407a3-d70c-4918-8ca8-59432e58f52e)
*<h5>IS2 Final (as of Jan. 27, 2024) 10-puzzle moving average of solve time (m), per puzzle day:*<br>
*Sun: 18.7, Mon: 5.0, Tue: 7.0, Wed: 9.2, Thu: 19.4, Fri: 13.5, Sat: 22.4*<br>


###

**Figure 3** shows IS1's solve time performance trajectory in violin plots with swarm plot overlays, broken out by 1-year solve date intervals. These representations may be somewhat easier to digest than the line plots in **Fig. 2**, as they remove the compressing effect of the long intervals with minimal solve activity. They also have the advantage of providing a clear visual sense of the number of solves and distribution shapes, per interval. Violin plots show both the range (vertical extent) and distribution characteristics (width as it varies across the y-axis range) for each puzzle day, per solve interval. Black lines on the violin plots demarcate solve time quartiles per puzzle day. Swarm plot overlays per puzzle day show individual puzzle raw solve times. The narrow geometries of the later week violin plots relative to the earlier week ones correspond to greater relative performance variability on those solve days. This phenomenon will be discussed in the final section of the summary in the context of correlation between past and future performance and prospects for predictive modeling. 

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

**Figure 5** shows per puzzle day scatterplots of raw GMSTs (x-axis) versus raw IS2 (y-axis) solve times. Points falling on the dashed diagonal line represent identical raw solve times for IS2 and GMST on a given puzzle. Points above and below this line represent "wins" for the GMS and IS2, respectively. IS2 win % across all puzzle days improved greatly from the pre-2023 (28.7%) to 2023/24 interval (50.0%). Win %s for IS2 also increased dramatically for most puzzle days in 2023/24, including a >2x increase for both Tuesday (34.6% to 71.6%) and Saturday (13.7% to 30.2%). The lowest IS2 win % for both time intervals was for Saturday, and Monday yielded the highest and second highest IS2 win %s in the pre-2023 and 2023/24 intervals, respectively (48% and 65%). The mean magnitude of performance advantage for the GMS over IS2 also decreased considerably in the more recent solve interval for all puzzle days together (6.1 to 2.2 minutes), as well as for all individual puzzle days (with IS2 gaining the advantage by this measure from Mon-Wed). Finally, per puzzle day regression lines show that there was a relatively high degree of correlation for raw solve times between IS2 and GMST (range across individual puzzle days and solve intervals: .54-.82). The next figure addresses this correlation in a way that is normalized for recent (prior to a give solve) baseline performance, per solver. This is particularly useful for IS2, since this solver solved many older puzzles in 2023-2024. Thus, the GMS was earlier on "their" own improvement curve when solving the same puzzles.   

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
###
The next correlational analysis was aimed at assessing the potential predictive value of IS2's baseline-adjusted past performance against specific constructors on their future performance against the same constructor. **Figure 8** shows this correlation between IS2 past performance (as mean % difference from RPB) against a given constructor (x-axis) and performance on the next solved individual puzzle by that constructor (y-axis). This analysis was restricted to only the n= puzzles by the constructor included in **Fig. 7** that were solved *after* >=3 previous puzzles by the same constructor (based on puzzle completion date for IS2, but issue date for GMS). There was a weak-to-moderate positive correlation for IS2 (r=.20), and a stronger one for GMS (r=.30). This weaker correlation for the individual solver relative to the GMS was also seen for IS1 (see link to analysis in Introduction). This disparity may have been due to the fact that performance for a single solver is inherently subject to more puzzle-to-puzzle variability than that of an "aggregate solver". Regardless, the evident positive correlations for all 3 solvers at relatively low puzzle n's provides optimism that including past performance vs constructor will have predictive value in the modeling phase.     

**Figure 8. IS2 and GMS: Past Performance Against Individual Constructors as "Prediction" of Next Puzzle Performance Against the Same Constructor**  

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/6dc42b32-97d9-4583-bf03-4fc0d5e6e2ff)
<h5>Pearson correlation coefficient (r): IS2: .20, GMS: .30

### IS1 Performance by Completion Time of Day

Many external variables are likely to have an impact on individual solver performance, for the large majority of which data collection would be very difficult. Examples include data relevant to how tired, stressed, influenced by caffeine and other substances, or distracted by other sensory stimuli the solver was while working on a given puzzle. The hardware technology used to solve a given puzzle (e.g., phone vs tablet vs computer) will also likely influence solve times in idiosyncratic ways. One external variable that we *are* fortunate to have data on (thanks, once again, to Matt at XWord Stats) is time of day at puzzle completion. **Figure 9** shows IS2's solve performance by hour of day, overall (black) and by puzzle day (by color). To control for day-specific puzzle difficulty, solve times are expressed as % difference from puzzle day-specific recent performance baseline (RPB). 

The majority of IS2 solves occurred in the evening (64.7% after 6 PM and 36.5% after 9 PM). One interesting trend was that very few solves between 12-8 AM (1/80; 1.3%) were "very fast" (>=50% faster than day-specific RPB). In contrast, 67/501 (13.4%) solves between 8-11 PM qualified as "very fast". So while there was no striking overall relationship between solve time and hour of completion, IS2's top performances were much more likely to come in the evening than late at night or in the early morning. Nonetheless, interpretation of this result is still difficult because puzzle *start* times were not available. Thus, it can't be distinguished with the available data whether IS2 was a better performer at night or simply finished easier puzzles before bedtime and left harder ones for morning completion. Another caveat is that all solve times were recorded with respect to the US Eastern Time Zone, and there is no indication for if/when individual puzzles were completed in other time zones.    

**Figure 9. Baseline-Adjusted Solve Times by Hour of Completion**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/b7b41555-d01b-489a-9182-517dbe191924)
*<h5>Times are all US Eastern Time Zone, adjusted for Daylight Savings Time as necessary.*

### Correlations of IS2 Performance on Individual Puzzles to Puzzle-Specific Features and Recent Past Performance

Numerous potentially interesting features pertaining to puzzle grids, clues, and answers were obtained from XWord Info across the sample period. Features showing strong correlation to IS2 solve performance become promising candidates as input features for predictive modeling, in current forms and/or when combined in novel ways with other existing features. **Figure 10** shows correlation heatmapping separately for 15x15 puzzles (Mon-Sat) and 21x21 puzzles (Sun) for a subset of all measured features with distributions amenable to linear regression and correlation analysis (see **Supplementary Figure 2** for individual 15x15 puzzle day matrices). The Pearson correlation coefficient (r) captures linear correlation strength between a given feature and solve times (top row and leftmost column of correlation matrix; red indicates a strong positive correlation and green a strong negative correlation). The rightmost column/bottom row per matrix shows the correlation between IS2 solve times for individual puzzles and puzzle day-specific recent performance baseline (RPB). For both 15x15 puzzles and 21x21 puzzles, this (positive) correlation was stronger than any other measured feature correlation to IS2 solve time. This finding generates a prediction that recent (relative to a puzzle date to be predicted) solver form per puzzle day will be more predictive of performance on a novel puzzle than will be any individual grid, clue or answer feature. 

As can also be seen in the **Fig. 10** correlation matrices, a number of grid, clue and answer-related features correlated strongly with each other. For example, 'Average Answer Length' and 'Freshness Factor' showed a strong negative correlation. This relationship makes intuitive sense because 'Freshness Factor' is a measure of aggregate answer rarity for a given puzzle, and longer answers have a higher likelihood of being uncommon than shorter ones. Additionally, numerous features not selected for this analysis might still be useful in predictive modeling but either had non-continuous distributions (e.g., 0 or 1 for puzzles with normal vs non-standard symmetry) or pertain to a feature that is largely specific to only one or several puzzle days (e.g. Rebuses, Circles, Shaded Squares; see **Supplementary Figures 3-5**). 

**Figure 10. Correlation Heatmapping of IS2 Raw Solve Times vs Grid, Clue, Answer and Past Performance Features**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/da0530f2-da5d-4785-95e4-1d0a654049b0)
*<h5>Correlation heatmaps derived from N=839 15x15 (left panel) and N=134 21x21 (right panel) puzzles solved by IS2 from 2020-2024.*

*Note on Inclusion Time Range*: As is clear in **Fig. 10**, RPB had the strongest correlation to individual solve times of any feature evaluated by a considerable degree. As such, there was a concern that shifts in baseline solve speed could overwhelm or mask correlations with puzzle-specific features. But normalizing raw solve times (e.g., with RPB) cancels out cross-puzzle day trends that I was interested in identifying prior to the modeling stage. As such, I arrived at a compromise in which I removed all solves from the first solve interval (2018/2019; n=98), which reduced baseline volatility in the solve pool to a considerable degree and allowed me to keep raw solve times as the y-axis variable across these analyses.*


###

**Figure 11** through **Figure 22** are companion figures to the correlation heatmapping shown in **Fig. 10**. These figures show, across all 15x15 puzzle days (black) and by puzzle day (colored), scatterplots of select features of interest vs IS2 raw solve times at the level of individual puzzles. A feature distribution density plot (FDP) shows puzzle day-specific trends in the distribution of each plotted feature. 

Though most features had at least moderate strength correlations to IS2 solve times across all 15x15 puzzles, at the by puzzle day level these correlations were typically stronger for the more difficult puzzle days (Sat, in particular). Correlations robust enough to show through within a given puzzle day, where many variables related to puzzle difficulty presumably had similar properties across puzzles, are likely to have a meaningful impact on solve times. As is evident across the scatterplot figures below, several factors make it more likely for later week puzzle days (e.g., Sat) to show within-day correlations that may also be associated with predictive value. For one, there may have been threshold values per feature below/above which that feature's impact was not significant in comparison with the contribution of solver aptitude (see discussion above about **Fig. 10**, and also see **Fig. 22**). Because late week puzzle days almost uniformly had considerably wider ranges of feature values than earlier week puzzle days (compare per day widths in the FDPs or x-axis extents in the scatterplots), effects apparent on those late week days may have been severely clipped by limited ranges on the early week days. Secondly, early week puzzles may also simply have not been difficult enough overall for given features (especially grid features, as a clue is only as difficult as the answer content that it houses) to have had discernable impacts on solve times.        

Each figure caption for **Figs. 11-22** compares the correlation strength for a given feature for IS2 with that for the global median solver (GMS) over the same set of puzzles. While GMS correlations were uniformly directionally the same as for IS2, they were also uniformly *stronger* than those for IS2. This relative strength was likely related to the more variable per day baseline solve performance of IS2 relative to the GMS (**see Figs. 1-4**), which in turn relates to one being a single human subject to puzzle-to-puzzle variability in many aspects and the other being a "mathematical entity" selected from many individual solvers on a given puzzle for being right in the middle of solve performance on that puzzle.


#### Scatterplots for Individual Features vs IS2 Solve Times, with Associated Feature Distribution Density Plots (FDPs)

#### *Grid Features*

**Figure 11. Number of Answers**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/6681923b-d32a-4ecf-9c48-7849a15e988c)
*<h5>Individual Solver 2 (IS2) solve times and '# Answers' had a moderately strong negative correlation for 15x15 puzzles (r= -.48).<br>
Global Median Solver (GMS) correlation strength on the same set of 15x15 puzzles was stronger (r = -.55).<br>*

*Most of the strength of the all 15x15 puzzles correlation (black) was related to the large leftward shift in the FDP for the two most difficult puzzle days (Fri and Sat). '# Answers' was strongly negatively correlated with 'Average Answer Length' (see Fig. 9) and measures of answer rarity (e.g., 'Freshness Factor'; see Fig. 20). Thus, when puzzles were difficult (Fri and Sat), this fewer answers/more long answers combination meant more answers that were rarely encountered/unique. Correlations of the reverse sign (positive) were seen for the early week puzzle days, particularly prominently for both Wednesday and the easiest puzzle day (Monday). This finding suggests that, below a particular per-clue/answer difficulty threshold mostly only attained in later week puzzles, the time penalty incurred by having to read relatively more clues was greater than the time savings from encountering relatively fewer longer answers.*       

**<h4>Figure 12. Number of Open Squares**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/e762b4ec-582d-44db-bf0d-0a3222bc7cd6)
*<h5>IS2 solve times and '# Open Squares' had a moderately strong positive correlation for 15x15 puzzles (r= .51).<br>
GMS correlation strength on the same set of 15x15 puzzles was stronger (r = .56).<br>*

*'# Open Squares' is a proprietary measure from XWord Info that counts all white squares that are *not* bordered by black squares. Most of the strength of the all 15x15 puzzles correlation (black) was related to the large rightward shift in the FDP for the two most difficult puzzle days (Fri and Sat), with the large majority of 15x15 puzzles with >~80 open squares falling on those days. '# Open Squares' was strongly negatively correlated with '# Answers' and strongly positively correlated with '#Average Answer Length' (see Fig. 10). For difficult puzzle days (Fri and Sat), these relationships translated to longer answers that were also more difficult. Within-day correlations were generally weak and of mixed sign, though Saturday had a positive correlation of roughly the same strength as the all 15x15 puzzles correlation. Given that the Saturday feature value range was much broader than that for the other 15x 15 puzzle days, there may have been difficulty and feature range effects at play here (see text above this section for context).*    
 

**<h4>Figure 13. Number of Black Squares**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/0abfd222-be2d-405d-a0e7-5c75802c235b)
*<h5>IS2 solve times and '# Black Squares' had a weak-to-moderate negative correlation for 15x15 puzzles (r= -.29).<br>
GMS correlation strength on the same set of 15x15 puzzles was stronger (r = -.38).<br>*

*Most of the strength of the all 15x15 puzzles correlation (black) was related to the large leftward shift in the FDP for the two most difficult puzzle days (Fri and Sat), with nearly all 15x15 puzzles with <~32 black squares falling on those days. '# Black Squares' was strongly negatively correlated with both '# Open Squares' and 'Average Answer Length'. So an increase in '# Black Squares' meant shorter, easier answers and a faster solve on average. Within Saturday a relatively strong correlation of the same directionality as the overall 15x15 puzzles correlation was seen, emphasizing these dynamics. The weak-to-nonexistent correlations on the earlier week puzzle days might indicate a difficulty threshold for '# Black Squares' to have an impact on solve times, though the lack of puzzles with <~32 black squares on early week puzzle days makes it hard to discern that from a range effect.*


**<h4>Figure 14. Average Answer Length**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/743958b6-321c-46d4-b31e-6cbe6c167958)
*<h5>IS2 solve times and 'Average Answer Length' had a moderately strong positive correlation for 15x15 puzzles (r= .58).<br>
GMS correlation strength on the same set of 15x15 puzzles was stronger, reaching the level of strong correlation (r = .67).<br>*

*The strong all 15x15 puzzles correlation was related to the large rightward shift in the FDP for the two most difficult puzzle days (Fri and Sat). Saturday also showed a relatively strong positive correlation across a wide range of feature values, with higher 'Average Answer Length' being associated with slower solves. As discussed in the contexts of Figs. 11 and 12, 'Average Answer Length' was strongly negatively correlated with '# Answers' and strongly positively correlated with measures of answer rarity (e.g. 'Freshness Factor; see Fig. 20). So it makes intuitive sense that as 'Average Answer Length' increased, particularly on difficult puzzle days, the answers themelves became more difficult and slowed down solve times even as they decreased in absolute number.* 

*Another interesting observation regarding this feature is that, unlike for the other grid features discussed thus far, the Thursday peak was well-differentiated to the right of those for the earlier week puzzle days in the FDP. Given the relatively strong positive correlations overall and for several late week puzzle days with wide feature value ranges (including Thursday), plus the need to explain why solve times for Thursday were well right-shifted from the earlier week puzzle days (see Figs. 2 and 4), this feature becomes an attractive candidate for having some predictive value across multiple puzzle days in the modeling phase.*  


**<h4>Figure 15. Number of Cheater Squares**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/be88ea7b-1acf-40e5-8a76-7c873ed00fd1)
*<h5>IS2 solve times and '# Cheater Squares' had a weak positive correlation for 15x15 puzzles (r= .14).<br>
GMS correlation strength on the same set of 15x15 puzzles was stronger (r = .20).<br>*

*Cheater Squares are black squares than can be removed without affecting the overall word count of the grid. These squares make construction easier (hence their name). It can be seen in the FDP that large numbers of them (>~10) almost exclusively appeared on the difficult puzzle days (Fri and Sat), which likely accounted for the (modest) positive correlation across all 15x15 puzzles. Saturday, with by far the widest feature value range of any of the 15x15 puzzle days, showed a moderate reverse sign (negative) correlation. This is not really at odds with the overall 15x15 positive correlation, since these squares are ultimately just black squares even if they facilitate tricky constructions for difficult puzzles. Add enough of them and they will reduce solve time simply by lowering the amount of fill. Incidentally, the reason cheater squares were only rarely seen in odd numbers is the NYT general requirement for grid symmetry.*

#### *Answer and Clue Content Features*

**<h4>Figure 16. Number of Fill-in-the-Blank Answers**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/80825453-04b6-42bd-bd80-2c4d62cf86a5)
*<h5>IS2 solve times and '# Fill-in-the-Blank Answers' had a weak-to-moderate negative correlation for 15x15 puzzles (r= -.25).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = -.26).<br>*

*In the all 15x15 puzzles scatterplot, a fairly dramatic drop in solve times can be seen for puzzles employing >=7 fill-in -the-blank clues, the large majority of which occured on the early week puzzle days. There were also modest negative correlations in later week puzzle days, suggesting that for IS2 larger numbers of fill-in-the-blank clues on difficult puzzles may have aided in speedier solves. The relative weakness of the correlations and the rarity of more difficult puzzles with large '# Fill-in-the-Blank', however, makes it difficult to have confidence that this feature will add much accuracy to a predictive model of solve times.* 

**<h4>Figure 17. Scrabble Average**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/74551179-8b84-4f7e-871c-5b17392ddba1)
*<h5>IS2 solve times and 'Scrabble Average' had a weak-to-nonexistent negative correlation for 15x15 puzzles (r= <-.01).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = -.03).<br>*

*'Scrabble Average' is another proprietary XWord Info measure, in which each letter in the answer grid is assigned its equivalent value in Scrabble. Since tile values in Scrabble increase with rarity of letter frequency in English texts, it would make sense that a higher value for this feature would be associated with *answers* of greater rarity. However, 'Scrabble Average' had only moderate positive correlations with other more direct measures of answer rarity both across 15x15 puzzles (Fig. 10) and specifically within the later-week puzzle days (Supp. Fig. 1). Given that these more direct measures of answer rarity DID have strong positive correlations to solve times (see Figs. 18-20), and that the correlation of 'Scrabble Average' itself to IS2 solve times across puzzle days was weak, this feature is a candidate to be left out of predictive modeling entirely.*

**<h4>Figure 18. Number of Scrabble Illegal Answers**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/62db9b7a-8b7c-4cc8-9c37-210708712cb0)
*<h5>IS2 solve times and '# Scrabble Illegal' had a weak positive correlation for 15x15 puzzles (r= .13).<br>
GMS correlation strength on the same set of 15x15 puzzles was stronger (r = .19).<br>*

*'# Scrabble Illegal' answers is a proprietary measure of XWord Info that gets at answer rarity more directly than does 'Scrabble Average'. Interestingly, the distributions for 15x15 puzzle days in the FDP were highly overlapping, other than a small leftward shift for Monday that likely accounted for the (modest) overall 15x15 puzzles positive correlation. '# Scrabble Illegal" had only moderate positive correlations with the most direct measures of answer rarity ('# Unique Answers' and 'Freshness Factor'; see Figs. 19 and 20), which was somewhat surprising to me. There were hints, particularly in the Monday and Saturday correlation plots, that this feature might have impacted solve times at the extreme low and high ends of its value range. However, the weak overall and within-day correlations to IS2 solve times shown by this feature suggest that more non-standard vocabulary *alone* may not strongly signify or predict puzzle difficulty.*     
 

**<h4>Figure 19. Number of Unique Answers**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/7d9121fd-91d4-4368-886f-25131d8dc17a)
*<h5>IS2 solve times and '# Unique Answers' had a weak-to-moderate positive correlation for 15x15 puzzles (r= .31).<br>
GMS correlation strength on the same set of 15x15 puzzles was stronger (r = .38).<br>*

*<h5>A unique answer is defined here as one that does not appear in any other NYT crossword puzzle in either the Shortz or pre-Shortz eras (either before or after the puzzle release date). The (albeit modest) strength of the all 15x15 puzzle day correlation was related to the easiest puzzle day (Monday) having a leftward shift in the FDP while the most difficult puzzle days (Fri and Sat) had rightward shifts. Given the relatively low correlations and the results shown in the next figure, uniqueness is perhaps an overly stringent criterion with which to define answer rarity. However, as evidenced in the all 15x15 puzzles scatterplot, there may still be some use for this feature in the predictive modeling phase when values reach both extremes of the range*

**<h4>Figure 20. Freshness Factor**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/add20189-632a-4726-96a5-f62a66652ba2)
*<h5>IS2 solve times and 'Freshness Factor' had a moderately strong positive correlation for 15x15 puzzles (r= .58).<br>
GMS correlation strength on the same set of 15x15 puzzles was considerably stronger, reaching the level of strong correlation (r = .67).<br>*

*<h5>'Freshness Factor' is a proprietary XWord Info measure that assesses the aggregate relative novelty of all answers in a given crossword puzzle as compared to those in all other crossword puzzles in the NYT archive. The much stronger correlation to IS2's solve times as compared to that for '# Unique Answers' suggests that there's much to be gained by taking a graded, as opposed to all-or-none, approach in assessing answer rarity. Overall, this feature had the strongest correlation with GMS solve times of any grid, clue or answer feature evaluated (but see Fig. 22 for a past performance feature with a stronger correlation to solve time).* 

*Additionally, with potential relevance to predictive modeling, the 15x15 puzzle days peaked in this measure (seen in the FDP) in relatively close concordance to the by day peaks in raw solve times (see **Figs. 2 and 4**) for IS2. The only other puzzle feature coming close to this degree and concordance of peak separation was 'Average Answer Length', though 'Freshness Factor' showed a Monday-Tuesday separation more in line with the solve time peaks separation for those two easy puzzle days. The positive correlation for this feature was also seen to a relatively consistent degree within each of the individual puzzle days beyond the two easiest (Mon and Tues). Saturday, strikingly, had both the strongest within-day correlation and also the widest range of feature values of any individual puzzle day. The observations discussed here lead me to believe that 'Freshness Factor' will be the most useful puzzle feature evaluated presently in terms of predictive modeling of solve performance.*



**<h4>Figure 21. Number of Wordplay Clues**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/c4bd003b-6769-4be3-9e0d-3d99d87cbc39)
*<h5>IS2 solve times and '# Wordplay Clues' had a moderate positive correlation for 15x15 puzzles (r= .32).<br>
GMS correlation strength on the same set of 15x15 puzzles was substantially stronger (r = .45).<br>*

*<h5>'# Wordplay' clues is an (admittedly) somewhat subjective measure that I have manually evaluated and calculated clue-by-clue across (most of) the entire puzzle sample completed by IS2. The FDP for this feature had some interesting properties, including the clear result that later week (Thu-Sat) puzzles indeed had a larger allocation of 'trickier' clues than early week puzzles. The was also a prominent leftward shift for Monday puzzles, though with a strong second peak aligned with the Tuesday peak. Taken together, these early and late week distribution offsets were likely related to the moderate overall positive correlation across all 15x15 puzzles. Additionally, IS2 (like both the GMS and IS1) had a clear trend toward slower solves on the easiest puzzle day (Mon) with unusually high '#Wordplay Clues'. For the other two solvers, this trend also extended to Tuesday.* 

**<h4>Figure 22. Decay-Time Weighted Recent Performance (RPB)**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/5cd044ff-389c-4d1e-8104-9978a91817c5)
*<h5>IS2 next raw solve time and IS2 'Recent Performance Baseline (RPB)' had a strong positive correlation on 15x15 puzzles (r= .73).<br>
GMS next raw solve time and GMS 'RPB' correlation strength was stronger, reaching the level of very strong correlation (r = .87).<br>*

*<h5>The all 15x15 puzzles correlation for this past performance feature was considerably stronger than that for any puzzle feature (Figs. 11-21). The implication is that time decay-time weighted IS2 recent past performance (RPB over the 20 day-specific puzzles previous to a given solve) will likely have more predictive value for the next IS2 raw solve time than will any single puzzle, clue or answer feature. Not all puzzle days were created equally, however, with regard to correlational strength (and, potentially, predictive power) of RPB and next raw solve time for this solver. Monday (r=.49) having the strongest correlation of the 15x15 puzzle days was unsurprising, given how few "degrees of freedom" there were in the easiest puzzles. This was also the 15x15 puzzle day with the strongest correlation for both the GMS and IS1. In the same vein, the two other easiest puzzle days, Tuesday (r=.47) and Wednesday (r=.44), followed closely behind Monday for IS1. Tuesday also had the second highest correlation for both the GMS and IS1.* 

*Interestingly, all 3 solvers had relatively low correlations for Thursday. That puzzle day had the second lowest correlation of any puzzle day for IS2 and the GMS, and the lowest by a wide margin for IS1 (a miniscule .15). This is perhaps unsurprising, since Thursday arguably had the largest degree of heterogeneity of any puzzle day, with nearly all puzzles on that day involving a gimmick or trick of some variety (including rebuses of various flavors; see Supp. Fig. 3). Also of note for the GMS was the standout low correlation for Saturday (.22). My suspicion is that this largely related to the volatility of the Saturday solver pool that the GMS was drawn from. Because Saturday was considerably more difficult than the other puzzle days, there may have been both a lower N to draw from for any given puzzle as well as a much more variable roster of puzzle completers. Of course, there may also have been a substantial contribution to the relatively low Saturday correlation for the GMS from the heterogeneity of Saturday puzzles (e.g., typically wide feature value ranges) and the high likelihood of middle-of-the-pack solvers getting "stuck" for extended stretches on one or several tough clues or answers.* 

*<h5> Next raw solve time and 'RPB' Correlation Strength by Solver (IS1 or GMS) and Puzzle Day:*<br>
*IS2: Sun: .45, Mon: .49, Tue: .46, Wed: .44, Thu: .32, Fri: .30, Sat: .38*<br>
*GMS: Sun: .55, Mon: .59, Tue: .49, Wed: .39, Thu: .35, Fri: .40, Sat: .22*<br>


# Supplementary Figures

**<h4>Figure S1. IS2 10-Puzzle Solve Time Moving Averages Adjusted by GMS Performance, by Puzzle Day** 

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/b94085ab-51c4-4457-9431-049c06a7d2f8)
*<h5>For each puzzle completed by IS2, % difference for the raw solve time from the global median solve time (GMST) was computed. The 10-puzzle moving average of this difference was then plotted, per puzzle day, by completion date. The volatility present in the raw solve times (see **Fig. 2 and Fig. 4**), including the upward spike in Q2-early Q3 2023, was still mostly present in these adjusted data plots, indicating that this volatility was due to factors other than by chance stretches of puzzles with substantially greater or lesser difficulty per puzzle day.*

**<h4>Figure S2. Correlation Heatmapping of IS2 Individual Puzzle Performance vs Grid, Answer and Past Performance Features by Puzzle Day (15x15 Puzzle Days)**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/390d8df0-a463-4d7d-96b0-fc21e7636cbb)


**<h4>Figure S3. Number of Rebus Squares vs IS2 Solve Time by Puzzle Day**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/3b64dac2-c4f7-49ab-a1ac-0dd31f1faf61)
*<h5>Only Thursday had an appreciable '# Rebus Squares' for IS2 solves. Rebus squares are those that must be filled with more than one letter, number or symbol for a given puzzle to be solved. There was a weak-to-moderate positive correlation for IS1 and a moderate one for GMS for Thursday, though a caveat is that the very large number of 0 rebus puzzles makes these correlations hard to interpret (ie, these are not exactly continuous distributions).*<br>

*Correlation Strength by Puzzle Day: IS2: Thu: .18; GMS: Thu: .27* 

**<h4>Figure S4. Number of Circled Squares vs IS2 Solve Time by Puzzle Day**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/802844d7-3c2f-4053-a39c-7212e2b3ecff)
*<h5>Circled squares were virtually non-existent in the tougher (Fri and Sat) puzzles. The modest negative correlation seen across all 15x15 puzzle days (-.12) is attributable to the fact that most 15x15 puzzles with circles appeared early in the week. The smattering of puzzles with circles on Sunday almost all fell in the middle of the solve time range regardless of "# Circles", indicating that this feature didn't likely have a major impact on solve times.*

**<h4>Figure S5. Number of Shaded Squares vs IS2 Solve Time by Puzzle Day**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2/assets/90933302/2ce5b8b8-8a9d-46b0-bef6-a821c014c6ce)
*<h5>Shaded squares, like circled squares, were virtually non-existent in the tougher (Fri and Sat) puzzles. Also like with circled squares, their function is to reveal a puzzle theme and their presence may provide assistance to solvers on clues in which they are embedded. Most puzzles with shaded squares were within the bottom third of IS2 15x15 puzzle solve times, most likely due to shaded squares almost exclusively showing up only in early week puzzles. Also as with '# Circles', the smattering of Sunday puzzles almost all fell in the middle of the solve time range regardless of "# Shaded Squares", indicating that this feature also isn't likely having a major impact on solve times.* 










