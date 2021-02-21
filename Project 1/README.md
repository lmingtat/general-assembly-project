# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) SAT and ACT Analysis for Year 2017 and 2018

### Problem Statement

The College Board is a non-profit that connects students to college success and opportunity. As part of our work, we want to track statewide participation and recommend where money is best spent to improve SAT participation rates. It is important to address this because this affects the future of all stakeholders, notably the future of the state and country itself.

Using data of SAT and ACT scores and participation rates from each state in the United States (from 2017 to 2018), we'll seek to identify trends in the data and combine our data analysis with outside research to identify likely factors influencing participation rates and scores in various states.

The state that we would like to work on is Iowa. Iowa has one of the lowest SAT participation (2-3%) along with one of the highest SAT total score, but is able to churn out one of the highest ACT composite scores (21.8-21.9) despite having mid-range participation in ACT.

### Executive Summary

In order to analyze our data, we imported our data and proceed to clean up for any outliers or incorrect input. Once done, an explratory data analysis was conducted to identify any trends between each features. Data visualisation using tables, histograms, scatterplots, boxplots and heatmap greatly helped to point out further insights. Once we have our data and observations sorted, we can pinpoint on how to help increase participations in Iowa. Refer to below for our insights and recommendations.

### Data Dictionary

|Feature|Type|Dataset|Description|
|:---|:----:|:---:|:---|
|State|Object|ACT|States that participate in ACT examination|
|Particpation|Int|ACT|Participation rate of students in each state taking part in the exam|
|English|Float|ACT|Scores of English test|
|Math|Float|ACT|Scores of Math test|
|Reading|Float|ACT|Scores of Reading test|
|Science|Float|ACT|Scores of Science test|
|Composite|Float|ACT|Composite score of each state|

|Feature|Type|Dataset|Description|
|:---|:----:|:---:|:---|
|State|Object|SAT|States that participate in SAT examination|
|Particpation|Int|SAT|Participation rate of students in each state taking part in the exam|
|Evidence-based_Reading_and_Writing|Int|SAT|Scores of Evidence-based Reading and Writing test|
|Math|Int|SAT|Scores of Math test|
|Total|Int|SAT|Total scores of each state|

### Conclusion/Recommendations

<u>Key findings from summarizing our observations:</u>
1. At the moment, more states do prefer to take ACT, but we can see that popularity with SAT rised year-on-year

2. Participation rate in one test is negatively correlated to the participation in the other test.
   SAT and ACT participations are mirror of each other.
   
2. Participation rate is negatively correlated to the change in score, vice-versa

3. Participation rate in one test is positively correlated to the change in score in the other test.  

Most states that have high participations in either tests are likely to have policies that mandate the participation in the test<sup>5</sup>. Students that are not college-bound will also take part, thus pulling down the average scores.
On the other hand, if participations are low, then this situation is likely due to students taking initative to undertake the exam in hopes of getting a high score and admission into college.

Another potential viewpoint that was observed is that Republican states are more biased towards ACT while Democratic states are more biased towards SAT. However, this needs to be further investigated. Further data would be required to check this relationship, such as percentage of democrat/republic demographic.

<u>Why Iowa?</u>
1. Iowa has one of the lowest SAT participation rate 

2. ACT composite scores are in top20 even with participation rate at approx 68%
   - we know that higher participation rate should have lower score, shows that Iowa bucked the trend
   
2. Iowa has a 91.4% high school graduation rate, best in the country<sup>6</sup>

3. Iowa has one of the lowest graduation requirement standards at the state level<sup>6</sup>

With a high base of students graduating out of high school, there is a bigger market to promote SAT to potential college-bound students. Subsequently we can also take up more market share from ACT.
Also, Iowa has one of the lowest graduation requirements, in that they do not require students to undertake ACT/SAT to graduate<sup>6</sup>. Hence, these students who take either tests are intending to go to college. 
This coupled with the Iowa's performance in the ACT tests, we can conjecture that these students are likely to be more studious and serious with the exam.
**Thus, it is aligned the College Board's mission to set these students up for college success and bring benefit to all stakeholders involved** (themselves, their family, the state and the country).

<u>Recommendations</u>
1. The College Board (CB) can contact the state of Iowa to sign a contract, such as Colorado or Illinois.  
   This strong push has also help SAT expand its market share<sup>7</sup>.  
   If the state of Iowa makes the SAT free for students who intends to go to college, then a proportion of students might not take ACT instead.
   
2. The high composite score of Iowa in the ACT can also be attributed to good teaching of covered topics in schools<sup>8</sup>. The CB should get better coaches to help train teachers in state schools. When the confidence level of the students or parents improve, then theoretically more students will partake in SAT.

3. Prepare test prep materials for students. Students in Iowa are currently ill-equipped for SAT, if this condition can be covered, then confidence level should rise as well.

4. Organize more career fairs in high schools to pique the students interest into taking college degrees. When students are more aware of possible career opportunities, then they might decide to enrol for college too.


### References
[1] https://co.chalkbeat.org/2020/7/13/21323566/colorado-offers-free-sat-dates-for-the-fall  
[2] https://www.denverpost.com/2017/03/06/colorado-juniors-sat-college-exam/  
[3] https://chicago.chalkbeat.org/2018/7/27/21105418/illinois-has-embraced-the-sat-and-the-act-is-mad-about-it  
[4] https://www.testive.com/illinois/  
[5] https://www.daytondailynews.com/news/historically-low-act-scores-red-flag-for-our-country/djfx9Urp719WyEaMfykyxL/
[5] https://www.testive.com/state-sat-act/  
[6] https://qconline.com/news/local/education/these-4-numbers-tell-the-story-of-public-education-in-iowa/collection_3e9751ea-8939-5dde-b95b-653f96c7ab47.html#1  
[7] https://www.washingtonpost.com/education/2018/10/23/sat-reclaims-title-most-widely-used-college-admission-test/  
[8] https://qctimes.com/news/local/education/the-numbers-iowa-s-average-act-score-is-21-6/article_5a62d78c-6744-5979-8de4-56b3d77bd1f0.html  
