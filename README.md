# DO_Campaigns
MMM Analysis

## Approach

Clean the data by removing user_id, session_id and utm_content which has 4,700 missing values out of 5,000 rows. Time spent per session (in minutes) is calculated using session_start_ts and session_end_ts. Several attribution models are available like, Last Interaction, First Interaction, Time Decay, Linear, or Position Based. However, a decision to choose a particular model need to be made by clarifying the details with the marketing teams. The way in which the interactions happen historically, need to be known. 

Monitoring the performance of the marketing efforts regularly and updating the attribution model is needed. Consumer behavior and market dynamics may change over time, so it is essential to adapt the strategies accordingly.

## Analysis

We need to analyze the customer journey to understand how customers interact with the marketing touchpoints before converting. Also, consider whether the journey is straightforward or involves multiple touchpoints across different channels.

Align the attribution model with the business goals. If the goal is to maximize immediate sales, a last-touch attribution model might be suitable. If the focus is on long-term brand awareness and engagement, a multi-touch attribution model might be more appropriate.

Assess the role and impact of each marketing channel in the customer journey. Some channels may serve as initial touchpoints to attract potential customers, while others may play a role in nurturing and converting leads. We need to choose an attribution model that accurately reflects the contribution of each channel. 

Different channels may have unique characteristics that influence how you attribute conversions. For instance, digital channels like search ads or social media ads often have clear tracking mechanisms, while offline channels like TV or print ads may require more estimation.

Depending on the availability and accuracy of data for each touchpoint, some attribution models may require more granular data and sophisticated tracking capabilities, which may not be feasible or accurate for all channels. This is one reason I chose to drop certain rows with missing data in the given csv file. 

We need to balance the complexity of the attribution model with the ease of implementation and interpretation. While more sophisticated models may provide a more nuanced understanding of customer behavior, simpler models may be easier to implement and communicate. 

## Model Considerations

The violin plots and histograms reveal a lot about the data and its underlying distribution. The data has several missing values & outliers. 

I chose the LightGBM Classifier due to the following reasons:
Fairly sophisticated Gradient Boosting Model yet simple enough to implement. The data is imbalanced with only 108 TRUE values for the target. Hence a Gradient Bosting model might perform the best without any a priory knowledge or sampling corrections, like over- or under-sampling to correct for the imbalance. LightGBM can also internally handle categorical data without explicitly converting those to dummy variables. Missing values & outliers can also be handled internally. 

However, the analysis requested to look into the various channels and campaigns about how these are affecting the target. Hence, I have explicitly created dummy varieables for specifically those variables: channel_id & utm_campaign. I have also removed rows missing values on features that we need to inquire.

## Metrics

I have chosen accuracy and Area Under the Curve (AUC) as two metrics. AUC is a much better choice here becausw we are dealing with a highly imbalanced dataset with too many negative cases. An f-score can also be used, depending on whether False Positives or False Negatives are more detrimental for the predictions.

## Conclusion

The LightGBM Classifier does not provide good results so this need to be improved using more experiments with larger and higher quality data and by discussing key results with the marketing team. The Feature Importances plot shows the created variable for Time Spent per session as the most important variable, followed by adwords_search, page, web_referral and others.

The Regressor for LightGBM was used to predict the time spent per session, which is in turn a proxy for website engagement. In lieu of lack of more granular data, like how much time is spent on specific activities in a particular page, I have decided to use time spent per session for measuring engagement. This particualr model is doing a good job of predicting the time spent with top features as page, adwords_search, utm_source followed by others. 

Adwords_search turns up as the most important channel, followed by web_referral. 

## Future Work
Budget is an important consideration for these campaigns, which is unkown. With more time in hand, other categorical variables can also be split into dummy variables to get a feature importance score attached to each category and necessary marketing steps can be taken accordingly. 

Investigate the outliers seen on the Violin plots for utm_term, medium, source & page by session time.

Most session time outliers apply to failed signups - are there technical glitches or is there a reason for this?

Data for content (blog posts, landing pages), website engagement metrics (page views, bounce rate) will enhance the attribution model. 

Parse the referrer field to match with utm_source - analyze if it is different.

Use HuggingFace Transformers to analyze utm_term further to decipher hidden intent of users.

I would also like to test different attribution models using historical data or A/B testing to evaluate their performance and accuracy. Eventually, comparing the results across models and choosing the one that best meets the objectives and providing actionable insights.

I can also learn how to get better quality data with fewer missing data and more data across time. Typically, I would like to divide the data by season, geography, and other demograpics to gain deeper insights. 


* [Full Noebook](https://github.com/agniji/DO_Campaigns/blob/main/AttribModel.ipynb)

