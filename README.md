# Design an A/B Test

## Experiment Design

### Metric Choice
List which metrics you will use as invariant metrics and evaluation metrics here. (These should be the same metrics you chose in the "Choosing Invariant Metrics" and "Choosing Evaluation Metrics" quizzes.)

Evalution metric defines the parameters thar are expected to change between the control and experimental group and the invariant metrics are used for sanity checking and they are not expected to change between the control and experimental group. 

- Invariant metrics: Number of Cookies, Number of clicks
- Evaluation metrics: Gross conversion,Retention, Net Conversion

For each metric, explain both why you did or did not use it as an invariant metric and why you did or did not use it as an evaluation metric. Also, state what results you will look for in your evaluation metrics in order to launch the experiment.

##### Number of Cookies

Number of cookies are the number of unique cookies to view course overview page. For this the unit of diversion is cookies, the number of cookies to view the course overview page will not be affected by the change made on 'Start free trial' button or after clicking the Start free trial, and can not be used as evaluation metric.

##### Number of clicks

Number of clicks is the number of unique cookies to click the 'Start free trail' button.Since the quations 'how many hours you devote for the coures ? ' comes after clicking 'Start free trail ' button , the number of clicks will not be expectd to change on the experimental group and hence it is an invariant metrics and can not be used as evaluation metric.

##### Gross conversion (GC)

Gross conversion is the number of user-ids to complete the checkout and enroll in the free trial divided  by the number of  unique cookies to click the 'Start free trial ' button. 

             GC = (Number of user-ids enrolled in free trail)/(Number of unique cookies)

In the experimental group, student will be enrolled after the question of how many hours should they devote per week,the number of enrolled user-id could be different from that of the control group and hence this metric is considered as an evaluation metric.

##### Retention (R)

Retention is the number of user-ids to remain enrolled past the 14-days boundary (and thus make at least one payment) divided by the number of user-ids to complete checkout and enrolled in the free trail. 
            
            R = (Number of user_ids past 14-days)/(Number of users who enrolled in the free trial)

Since the number of user-ids enrolled for the free trial in the experimental group could be affected by the pop-up webpage asking hours of devotion per week for the course, this metric would not be the same for both control and experimental groups , and therefore is an evaluation metric.

##### Net Conversion (NC)

Number of user-ids to remain enrolled past the 14-day boundary (and thus make at least one payment) divided by the number of unique cookies to click  the 'Start free trail'. 

          NC = (Number of user-ids remain enrolled past 14 days)/(Number of uniue cookies to click the 'Start free trial')

Eventhough the number of cookies to click the 'Start free trial' is the same for both control and experimental groups, the number of user-ids that enrolled passed the 14 day free trail boundary could be still affected by the question posed in the experimental group, hence this metric can be considered as an evaluation metric.



### Measuring Standard Deviation
List the standard deviation of each of your evaluation metrics. (These should be the answers from the "Calculating standard deviation" quiz.)

For each of your evaluation metrics, indicate whether you think the analytic estimate would be comparable to the the empirical variability, or whether you expect them to be different (in which case it might be worth doing an empirical estimate if there is time). Briefly give your reasoning in each case.

### Sizing
#### Number of Samples vs. Power
Indicate whether you will use the Bonferroni correction during your analysis phase, and give the number of pageviews you will need to power you experiment appropriately. (These should be the answers from the "Calculating Number of Pageviews" quiz.)

#### Duration vs. Exposure
Indicate what fraction of traffic you would divert to this experiment and, given this, how many days you would need to run the experiment. (These should be the answers from the "Choosing Duration and Exposure" quiz.)

Give your reasoning for the fraction you chose to divert. How risky do you think this experiment would be for Udacity?

## Experiment Analysis
### Sanity Checks
For each of your invariant metrics, give the 95% confidence interval for the value you expect to observe, the actual observed value, and whether the metric passes your sanity check. (These should be the answers from the "Sanity Checks" quiz.)

For any sanity check that did not pass, explain your best guess as to what went wrong based on the day-by-day data. Do not proceed to the rest of the analysis unless all sanity checks pass.

### Result Analysis
Effect Size Tests
For each of your evaluation metrics, give a 95% confidence interval around the difference between the experiment and control groups. Indicate whether each metric is statistically and practically significant. (These should be the answers from the "Effect Size Tests" quiz.)

### Sign Tests
For each of your evaluation metrics, do a sign test using the day-by-day data, and report the p-value of the sign test and whether the result is statistically significant. (These should be the answers from the "Sign Tests" quiz.)

## Summary
State whether you used the Bonferroni correction, and explain why or why not. If there are any discrepancies between the effect size hypothesis tests and the sign tests, describe the discrepancy and why you think it arose.

## Recommendation
Make a recommendation and briefly describe your reasoning.

## Follow-Up Experiment
Give a high-level description of the follow up experiment you would run, what your hypothesis would be, what metrics you would want to measure, what your unit of diversion would be, and your reasoning for these choices.

# Reference
1. [https://vwo.com/ab-testing/](https://vwo.com/ab-testing/)
2. [http://rajivgrover1984.blogspot.com/2015/11/ab-testing-overview.html](http://rajivgrover1984.blogspot.com/2015/11/ab-testing-overview.html)
3. []()
4.[]() 
