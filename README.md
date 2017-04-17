# Design an A/B Test
## 1 Experiment Design

1. Experiment Design

1.1 Metric Choice

List which metrics you will use as invariant metrics and evaluation metrics here.
-Invariant metrics: Number of cookies, Number of clicks
-Evaluation metrics: Gross conversion, Retention, Net conversion
For each metric, explain both why you did or did not use it as an invariant metric and why you did or did not use it as an evaluation metric. Also, state what results you will look for in your evaluation metrics in order to launch the experiment.
Number of cookies (Number of unique users to visit the course overview page): Unit of Diversion is cookies, it's evenly distributed in control and experiment group. Also, the visits happen before the users see the experiment and thus independent from it.
Number of clicks (Numer of unique cookies to click the start free trial button): As the click happen before the users see the experiement and independent from it. Explicitly speaking, the page asking the number of hours of the student devotion after clicking "Start free Trial" button, but the course overview page remains the same for both control & experiment group.
Gross conversion (Number of users who enrolled in the free trial/Number of users who clicked the Start Free Trial button): A good evaluation metrics since it's directly dependent on the effect of the experiment & allow us to show whether we managed to decrease the cost of enrolment aren't likely to be real customers. In detail, in the experiment group the user can make a decision, if he has enough time to devote for course, he will be enrolled or if not, he will continue with the free courseware without enrolling. Vice versa, for the control group, no pop-up would be displayed regardless of the time availability enrolls for the course. The underlying assumption would be the gross conversion in the control group is higher than experiment group Therefore, it can be used as an evaluation metric to check if the experiement makes a significant difference in the enrolment.
Retention (Number of user-ids to remain enrlled for 14 days trial period and make their first payment/Number of users who enrolled in the free trial): As mentioned in gross conversion metric, in the experiment group, users are completely aware of the time commitment, they made a deliberate decision to enrol the course or continue with the free courseware option. We expect to see the following result: The rentention might be high for the experiment group, since fewer users enrolled based on their time commitment & likely to to remain enrolled after 14-day period and start their first initial payment. But for the control group, many users enroll for the courseware, since not many of them have the required time, the cancellation rate might be high and hence the retention rate will be low.
Net conversion (Number of user-ids remained enrolled for 14 days trial and at least make their first payment/Number of users clicked the Start Free Trial button): For the experiment group, users aware of the time commitment requirement through the screener page and can make a decision to remain enrolled for the course past 14 days trial-period. However, on the control group side, they would be able to continue the payment wouthout aware of the minimum time requirement. Therfore, it can be used as Evaluation metric. The net conversion is the final result after previous two evaluation metrics: gross conversion & retention and we expect to see whether having a "5 or more hours per week" button help increase the ratio of user making payment over total people see the start free trial page.
Number of User-ID : Not an ideal metric for both evaluation & invariant metric. The number of users enrol in the free trial is dependent on the experiment, we expect to see different value in the control and experiment group, therefore it cannot be a good invariant metric. Meawhile, the number of visitors between experiement are likely to be different & number of enrolled user can fluctuate in a particular day, which likely to skew the result.
Click-through-probability : This is a good invariant metric since the clicks are occurred before the users see the experiment, therefore it is does not depend on our test which is an excellent invariant metric. However, I believe the number of cookies & number of clicks are already sufficient to use as invariant metric & extra metric is nice to have but may not be as critical as the other two.
The expectation for the experiment migh be as follow: the gross conversion will decrease practically significance, which indicate whether the cost will be lower by introducing the new screener; while net conversion will not decrease statistically significance, which indicate the screener whether or not affect the revenues.

1.2 Measuring Standard Deviation

List the standard deviation of each of your evaluation metrics
Calculation (Data):

+ Gross conversion: se = sqrt(0.20625*(1-0.20625)/3200) = 0.00715 (correspond to 3200 clicks & 40000 pageviews).
For 50000 pageviews, we have new_se = 0.00715 * sqrt(40000/5000) = 0.0202 
+ Retention: se = sqrt((0.53*(1-0.53)/660) * sqrt(40000/5000))) = 0.549
+ Net conversion: se = sqrt(0.1093125*(1-0.1093125)/3200) = 0.0055159 (correspond to 3200 clicks & 40000 pageviews).
For 50000 pageviews, we have new_se = 0.00715 * sqrt(40000/5000) = 0.0156 
Final Results:

Gross conversion: 0.0202
Retention: 0.0549
Net conversion: 0.0156
For each of your evaluation metrics, indicate whether you think the analytic estimate would be comparable to the the empirical variability, or whether you expect them to be different (in which case it might be worth doing an empirical estimate if there is time). Briefly give your reasoning in each case.
Both Gross Conversion and Net Conversion using number of cookies as denominator, which is also unit of diversion. Here, the unit of diversion is equal to unit of analysis, which indicate the analytical estimate would be comparable to the emperical variability.

For Retention, the denominator is "Number of users enrolled the courseware" which is not similar as Unit of Diversion. The unit of analysis and the unit of diversion are not the same therefore the analytical an the empirical estimates are different.

1.3 Sizing

1.3.1 Number of Samples vs. Power

Indicate whether you will use the Bonferroni correction during your analysis phase, and give the number of pageviews you will need to power you experiment appropriately.
No, I did not use Bonferronicorrection during my analysis phase. The metrics in the test has high correlation (covariant) and the Bonferroni correction will be too conservative to it.

After much consideration from back-of-the-envelope calculation, I realised the amount of pageview for retention as evaluation metrics would need almost half-a-year for testing even if we direct 50% of traffic to that experiment, which is completely not a economic feasible timeline for a A/B Testing result. Therefore, I have iterate my evaluation metrics and use Gross Conversion and Net Conversion as evaluation metrics. Using Evan Miller, the result can be referred below:

Probability of enrolling, given click:
20.625% base conversion rate, 1% min d.
Samples needed: 25,835

Probability of payment, given click:
10.93125% base conversion rate, 0.75% min d.
Samples needed: 27,413 (chosen)

Therefore, pageview/group = 27413/0.08 = 342662.5
Total pageview = 342662.5*2 = 685325
*Note1 : only 0.08 pageview leads to click.
*Note2: double pageview because we need total pageview for both experiment & control group
1.3.2 Duration vs. Exposure

Indicate what fraction of traffic you would divert to this experiment and, given this, how many days you would need to run the experiment.
With daily traffic of 40000, I'd direct 70% of my traffic (28000) to the experiment, which means it would take us approximately 25 days (685325/28000 = 25) for the experiment.

Give your reasoning for the fraction you chose to divert. How risky do you think this experiment would be for Udacity?
The experiment would not affect whole operation of existing paying customers as well as highly motivated students (I'd suspect comprised the majority of the net conversion) and also would not affect Udacity content. Therefore, the whole experiment would not considered as highly risky. However, I'd not direct all traffic to experiment to prevent small bug in the process.

2. Experiment Analysis (data)

2.1 Sanity Checks

For each of your invariant metrics, give the 95% confidence interval for the value you expect to observe, the actual observed value, and whether the metric passes your sanity check.
Calculation:

1. Number of cookies:
Total Control group pageview: 345543
Total Experiment group pageview: 344660 
Total pageview: 690203
Probability of cookie in control or experiment group: 0.5
SE = sqrt(0.5*(1-0.5)*(1/345543+1/344660) = 0.0006018
Margin of error (m) = SE * 1.96 = 0.0011796
Confidence Interval = [0.5-m,0.5+m] = [0.4988,0.5012]
Observed value  = 344660/690203 = 0.5006

2. Number of clicks: 
Total Control group clicks: 28378
Total Experiment group cliks: 28325
Total pageview: 56703
Probability of cookie in control or experiment group: 0.5
SE = sqrt(0.5*(1-0.5)*(1/28378+1/28325) = 0.0021
Margin of error (m) = SE * 1.96 = 0.0041
Confidence Interval = [0.5-m,0.5+m] = [0.4959,0.5041]
Observed value  = 28378/56703 = 0.50046
Results:

Number of cookies: [0.4988,0.5012]; observed .5006; PASS Sanity Check
Number of clicks : [0.4959,0.5041]; observed .50046; PASS Sanity Check
2.2 Result Analysis

2.2.1 Effect Size Tests

For each of your evaluation metrics, give a 95% confidence interval around the difference between the experiment and control groups. Indicate whether each metric is statistically and practically significant.
Gross Conversion:

Control Group	Experiment
Clicks	17293	17260
Enrolment	3785	3423
Gross Conversion	0.2188746892	0.1983198146
SE = 0.004371675385
m = SE * 1.96 = 0.00856848375
Pooled Probability = 0.2086
D hat = -0.02055
Confidence Interval = [-0.0291,-0.0120]

Result:

Gross conversion CI: [-.0291, -.0120]
- statistically significant (CI doesn't contain zero)
- practically significant (CI doesn't contain d_min value)
Control Group	Experiment
Clicks	17293	17260
Enrolment	2033	1945
Net Conversion	0.1175620193	0.1126882966
SE = 0.003434133513
m = SE * 1.96 = 0.0067
Pooled Probability = 0.2086
D hat = -0.0049
Confidence Interval = [-0.0116,-0.0018]
Result:

Net conversion CI: (-0.0116, 0.0018)
- not statistically significant (CI contains zero)
- not practically significant (CI contain d_min = +/- 0.0075)
2.2.2 Effect Size Tests

For each of your evaluation metrics, do a sign test using the day-by-day data, and report the p-value of the sign test and whether the result is statistically significant.
Gross Conversion:

Number of success: 4
Number of trials: 23
Probability: 0.5
Two-tailed p-value : 0.0026
p-value = 0.0026 < alpha level = 0.025. Therefore, we agree with the initial hypothesis, that the data is statistically and practically significant.

Net Conversion:

Number of success: 10
Number of trials: 23
Probability: 0.5
Two-tailed p-value : 0.6776
p-value = 0.6776 > alpha level = 0.025. Therefore, we agree with the initial hypothesis, that the net conversion CI is both statistically and practically insignificant.

2.2.3 Summary

State whether you used the Bonferroni correction, and explain why or why not. If there are any discrepancies between the effect size hypothesis tests and the sign tests, describe the discrepancy and why you think it arose.
Bonferroni correction was not used because the metrics in the test has high correlation (high variance) and the Bonferroni correction will be too conservative to it. I completely comprehend the importance to correct if a test is launched and the metrics shows a significant difference, because it's more liely that one of multiple metrics will be falsely positive as the number of metrics increases. However, we would only launch if all evaluation metrics must show a significant change. In that case, there would be no need to use Bonferroni correction. In other words, correction is applied if we are using OR on all metrics, but not if we are testing for AND of all metrics.

2.3 Recommendation:

Make a recommendation and briefly describe your reasoning.
My final recommendation is we should NOT launch the experiment. In order to back-up my recommendation, I'd like come up with 2 reasons:

Gross Conversion: the result have showned Gross Conversion turned out to be negative and practically significant; which is also expected since most people would be discouraged by the time requirement and unlikely to give a proper product trial. This is a good news for Udacity team since it'd lower the cost to take care of these leads which are unlikely to convert. Udacity coach can now focusing on more quality students and the probability of making first purchase after 14-days trial would increase.

Net Conversion: unfortunately, net conversion results are both statistically and practically insignificant and the confidence interval also includes negative numbers. My assumption is for the control group, although the users are not receiving the time requirement recommendation, but along 14 days trial period they have already awared of the time commitment and decided to opt-out. The users from the experiment group didn't get the psychological effect from the screener, also found no financial commitment for the courseware and also decided to try out, only to opt-out later. As a result, number of users making the payment in both group are statistically insignificant.

Based on the analysis & reasoning above, gross conversion result is a good outcome because the cost is lower by discouraging users who're unwilling to commmit and unlikely to convert. On the other hand, net conversion results ended up being bot statistically & practically insignificant while the confidence interval does include the negative number of the practical significance boundary; meaning, it's possible that this number went down by an amount that would hurt the business - decrease the revenue. If we consider the initial hypothesis, it does not increase numbers of paid users, which fails the inital goal of launching this feature and likely to be unacceptable risk to launch.

3. Follow-up experiment

Give a high-level description of the follow up experiment you would run, what your hypothesis would be, what metrics you would want to measure, what your unit of diversion would be, and your reasoning for these choices.
For myself as a Udacity student, I've experienced initial frustration for not meeting the prerequisite 1 year ago, when I was having no knowledge of Python and statistics at all. I ended up paying Udacity for 1 month without understand any course materials and not even able to understand the first project. This would leads me with so much frustration and decided to quit the program half-heartedly, concluded I was not meant to learn data analysis. Luckily, I found other resources and it helped me learned the foundation for the program and now I'm almost completeing the whole nanodegree. As a student, I know the feeling of being inadequate & inferior; thus, I proposed Udacity to launch a new initiative to help those students in need, which is: A new mini-course required students to complete the project within that 14 days trial. The course will cover basic knowledge of Python & Data Analysis which would be doable if the students spent minimum 10 hours/week. Through this mini-course, students know the level of fluency the nanodegree required and also act as an encouragement that if they willing to learn, course completion is a possible task.

Null hypothesis by creating such mini-course, it will not increase Retention by a practically significant amount.

The mini-course will be randomly assigned to a Control & Experiment Group. The whole courses for Control Group would not change and remained the same while courses for Experiment Group will have this one mini-course (which required them to finish within 14 days)

Unit of diversion is User-IDs, users once enrolled in this new mini-course will be tracked by user-id and this change only impacts what happens after a free trial account is created. The main purpose is we want users to only see this "new offering" one version at a time, and not to confuse user by showing diffrent version option at different time.

Invariant metric is number of cookies since unit of diversion is cookie, and because users are not exposed to this new course after hitting "Free Trials" screener button.

Evaluation metric is Net Conversion, whether rendering a "new mini-course" helps increase the ratio of users who make payment over those who decided only to try the program. If the CI shows practically and statistically significant, this will prove that this initiative will increase the eventual revenue by having more people signing up for the program.

If Net Conversion is positive and practically significant at the end of the experiment, we can roll out this new course to whole Nanodegree program and added the mini-course as the official course of Data Analyst nanodegree program.
