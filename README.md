# Design an A/B Test

## Experiment Design

### Metric Choice
<em><strong> List which metrics you will use as invariant metrics and evaluation metrics here. (These should be the same metrics you chose in the "Choosing Invariant Metrics" and "Choosing Evaluation Metrics" quizzes.) </strong> </em>

Evalution metric defines the parameters thar are expected to change between the control and experimental group and the invariant metrics are used for sanity checking and they are not expected to change between the control and experimental group. 

- Invariant metrics: Number of Cookies, Number of clicks
- Evaluation metrics: Gross conversion,Retention, Net Conversion

<em><strong> For each metric, explain both why you did or did not use it as an invariant metric and why you did or did not use it as an evaluation metric. Also, state what results you will look for in your evaluation metrics in order to launch the experiment.</strong> </em>

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
            
            R = (Number of user-ids past 14-days)/(Number of users who enrolled in the free trial)

Since the number of user-ids enrolled for the free trial in the experimental group could be affected by the pop-up webpage asking hours of devotion per week for the course, this metric would not be the same for both control and experimental groups , and therefore is an evaluation metric.

##### Net Conversion (NC)

Number of user-ids to remain enrolled past the 14-day boundary (and thus make at least one payment) divided by the number of unique cookies to click  the 'Start free trail'. 

          NC = (Number of user-ids remain enrolled past 14 days)/(Number of uniue cookies to click the 'Start free trial')

Eventhough the number of cookies to click the 'Start free trial' is the same for both control and experimental groups, the number of user-ids that enrolled passed the 14 day free trail boundary could be still affected by the question posed in the experimental group, hence this metric can be considered as an evaluation metric.

I will assess two evaluation meterics, the Gross Conversion and Net Convertion rate to check if  the pop up website  about the number of hours spent per weeks would reduce students frastration and results increase in the number of student which pass the 14-day free trial boundary.

### Measuring Standard Deviation
<em><strong> List the standard deviation of each of your evaluation metrics. (These should be the answers from the "Calculating standard deviation" quiz.)</strong> </em>

Based on the baseline values we can estimate Statandard deviation (SD) analytically for the two selected evaluation metrics, Gross conversion (GC) and Net Converison. Assuming a binomial distribution 
   
        SD = sqrt((p*(1-p)/N)
        
 For Gross Conersion
        
        N = 400, p = 0.2063 ,then SD = 0.0202
For net conversion   

       N = 400, p = 0.1093, SD = 0.0018
   

<em><strong> For each of your evaluation metrics, indicate whether you think the analytic estimate would be comparable to the the empirical variability, or whether you expect them to be different (in which case it might be worth doing an empirical estimate if there is time). Briefly give your reasoning in each case.</strong> </em>

To compute  both  Gross convertion and Net conversion metrics unique cookies that click the 'Start free' button are used as unit of anlyisis, which is similar to the unit of diversion that is unique cookies. As a matter of fact the the analytical esimate and empirical esitmate of variablity should be closer to each other.  

### Sizing
#### Number of Samples vs. Power
<em><strong> Indicate whether you will use the Bonferroni correction during your analysis phase, and give the number of pageviews you will need to power you experiment appropriately. (These should be the answers from the "Calculating Number of Pageviews" quiz.)</strong> </em>

I did not use Bonferronicorrection during my analysis phase. The metrics in the test has high correlation (covariant) and the Bonferroni correction will be too conservative to it.

 I used he online Sample Size calculator (http://www.evanmiller.org/ab-testing/sample-size.html). The baseline conversion rate is calcualted for each metrics  and the minimum detectable effect (dmin) are show below.
 
      Probability of enrolling given number of click (p): 20.625 % and dmin of 1 %
      Sample Size = 25,835
      
      Probability of payment given number of  click (p): 10.93125 % and dmin 0.75 %
      Sample Size = 27,413
      
Calculate the number of pageviews:Among 40000 page views only 3200 people click the 'Start free trail ' button, then the number of pageviews will be 
                  
     27,413 * 40000/3200 =  342,662.5
The total number of pageview needed for the two groups , control and experimental group is 
    
     342,662.5*2 = 685,325
 
Bonferroni correction will not be used as  both evaluation metrics have since Bonferroni correction is too conservative.

#### Duration vs. Exposure
<em><strong> Indicate what fraction of traffic you would divert to this experiment and, given this, how many days you would need to run the experiment. (These should be the answers from the "Choosing Duration and Exposure" quiz.)</strong> </em>

Considering the daily traffic of 40000, I would direct 75% of my traffic (30000) to the experiment and the total number of page views required for both control and experimental group is 685,325, which  means it would take us approximately 685325/30000 = 22.844 days for the experiment.

<em><strong> Give your reasoning for the fraction you chose to divert. How risky do you think this experiment would be for Udacity?</strong> </em>

Directing 75% of traffic to the experimental group required less number of days to run and since the experiment only poses a question about number of hours committed per week, it doesn't change any of the contents of udacity, the experiment has modest or no risk. 

## Experiment Analysis
### Sanity Checks
<em><strong> For each of your invariant metrics, give the 95% confidence interval for the value you expect to observe, the actual observed value, and whether the metric passes your sanity check. (These should be the answers from the "Sanity Checks" quiz.)</strong> </em>
      
      1. Number of cookies:
         Total pageviews for control group: 345543
         Total total pageviews for experimental group: 344660 
         Total pageviews: 690203
         Probability of cookie in control or experiment group: 0.5
         SE = sqrt(0.5*(1-0.5)*(1/345543+1/344660) = 0.0006018
         Margin of error (m) = SE * 1.96 = 0.0011796
         Confidence Interval = [0.5-m,0.5+m] = [0.4988,0.5012]
         Observed value  = 344660/690203 = 0.5006

     2. Number of clicks: 
        Total number of clicks for control group: 28378
        Total number of clicks for experimental group: 28325
        Total number of clicks: 56703
        Probability of cookie in control or experiment group: 0.5
        SE = sqrt(0.5*(1-0.5)*(1/28378+1/28325) = 0.0021
        Margin of error (m) = SE * 1.96 = 0.0041
        Confidence Interval = [0.5-m,0.5+m] = [0.4959,0.5041]
        Observed value  = 28378/56703 = 0.50046

<em><strong> For any sanity check that did not pass, explain your best guess as to what went wrong based on the day-by-day data. Do not proceed to the rest of the analysis unless all sanity checks pass.</strong> </em>

As calccualted above the confidence interval for number of cookies is between 0.4988 and 0.5012 where as the observed value is 0.5006 which lies between the lower and upper boun of the confidence interval and the confidence interval for number of cookies is 0.4959 and 0.5041 where as the observed value is 0.50046 which also lies between lower and upper bound of the confidence interval. We can say that both invariant meterics pass the sanity check.

## Result Analysis
### Effect Size Tests
<em><strong> For each of your evaluation metrics, give a 95% confidence interval around the difference between the experiment and control groups. Indicate whether each metric is statistically and practically significant. (These should be the answers from the "Effect Size Tests" quiz.)</strong> </em>

For Gross conversion:
    
    Clicks for control = 17293 ,  Clicks for experiment = 17260
    Enrollment for control = 3785, Enrollment for experiment = 3423
Then
  
    Gross conversion for control = 3785/17293 = 0.2188746892
    Gross Conversion for experiment = 3423/17260 = 0.1983198146
  
And for 95 % confidence interval the z-score = 1.96
    
    pooled probability = (0.2188746892+ 0.1983198146)/2  = 0.2085972519 
    SE = SD = sqrt((p_pool*(1-p_pool)/(1/N_exp + 1/N_cont)) = 0.004371599645
    dhat = 0.1983198146 - 0.2188746892 = -0.0205548746
    Marigin of error , m = z*SE = 1.96*0.004371599645 = 0.008568335303
    Confidence Interval : [-0.0291,-0.0120]
    
    
For Net conversion:
    
    Clicks for control = 17293 ,  Clicks for experiment = 17260
    Payment for control = 2033, Payment for experiment = 1945
Then
  
    Net conversion for control = 2033/17293 = 0.1175620193
    Net Conversion for experiment = 1945/17260 = 0.1126882966
  
And for 95 % confidence interval the z-score = 1.96
    
    pooled probability = (0.1175620193+ 0.1126882966)/2  = 0.115125158 
    SE = SD = sqrt((p_pool*(1-p_pool)/(1/N_exp + 1/N_cont)) = 0.003434103318
    dhat = 0.1126882966 - 0.1175620193 = -0.0049
    Marigin of error , m = z*SE = 1.96*0.003434103318 = 0.0067
    Confidence Interval : [-0.0116,-0.0018]
    

### Sign Tests
<em><strong> For each of your evaluation metrics, do a sign test using the day-by-day data, and report the p-value of the sign test and whether the result is statistically significant. (These should be the answers from the "Sign Tests" quiz.)</strong> </em>
I used the online calculator (http://graphpad.com/quickcalcs/binomial1.cfm) to perform sign tests. 

For Gross Conversion:
   
    Number of success: 4
    Number of trials: 23
    Probability: 0.5
    Two-tailed p-value : 0.0026
    
For Net Conversion:
  
    Number of success: 10
    Number of trials: 23
    Probability: 0.5
    Two-tailed p-value : 0.6776


## Summary
<em><strong> State whether you used the Bonferroni correction, and explain why or why not. If there are any discrepancies between the effect size hypothesis tests and the sign tests, describe the discrepancy and why you think it arose.</strong> </em>

## Recommendation
<em><strong> Make a recommendation and briefly describe your reasoning.</strong> </em>

## Follow-Up Experiment
<em><strong> Give a high-level description of the follow up experiment you would run, what your hypothesis would be, what metrics you would want to measure, what your unit of diversion would be, and your reasoning for these choices.</strong> </em>

# Reference
1. [https://vwo.com/ab-testing/](https://vwo.com/ab-testing/)
2. [http://rajivgrover1984.blogspot.com/2015/11/ab-testing-overview.html](http://rajivgrover1984.blogspot.com/2015/11/ab-testing-overview.html)
3. [https://blog.kissmetrics.com/ab-testing-introduction/](https://blog.kissmetrics.com/ab-testing-introduction/)
4. [http://larslofgren.com/growth/7-rules-for-ab-testing](http://larslofgren.com/growth/7-rules-for-ab-testing) 
