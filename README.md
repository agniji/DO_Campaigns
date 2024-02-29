# DO_Campaigns
MMM Analysis

## Approach

Clean the data by removing user_id, session_id and utm_content which has 4,700 missing values out of 5,000 rows. Time spent per session is calculated using session_start_ts and session_end_ts. Several attribution models are available like, Last Interaction, First Interaction, Time Decay, Linear, or Position Based. However, a decision to choose a particular model need to be made by clarifying the details with the marketing teams. 
Monitoring the performance of the marketing efforts regularly and updating the attribution model is needed. Consumer behavior and market dynamics may change over time, so it's essential to adapt the strategies accordingly.

We need to analyze the customer journey to understand how customers interact with the marketing touchpoints before converting. Also, consider whether the journey is straightforward or involves multiple touchpoints across different channels.

Align the attribution model with the business goals. If the goal is to maximize immediate sales, a last-touch attribution model might be suitable. If the focus is on long-term brand awareness and engagement, a multi-touch attribution model might be more appropriate.

Assess the role and impact of each marketing channel in the customer journey. Some channels may serve as initial touchpoints to attract potential customers, while others may play a role in nurturing and converting leads. We need to choose an attribution model that accurately reflects the contribution of each channel. 

Different channels may have unique characteristics that influence how you attribute conversions. For instance, digital channels like search ads or social media ads often have clear tracking mechanisms, while offline channels like TV or print ads may require more estimation.

Depending on the availability and accuracy of data for each touchpoint, some attribution models may require more granular data and sophisticated tracking capabilities, which may not be feasible or accurate for all channels. This is one reason I chose to drop certain rows with missing data in the given csv file. 

We need to balance the complexity of the attribution model with the ease of implementation and interpretation. While more sophisticated models may provide a more nuanced understanding of customer behavior, simpler models may be easier to implement and communicate. 

I chose the LightGBM Classifier due to the following reasons:
Fairly sophisticated Gradient Boosting Model yet simple enough to implement. The data is imbalanced with only 108 TRUE values for the target. Hence a Gradient Bosting model might perform the best without any apriory knowledge or sampling corrections, like over- or undersampling to correct for the imbalance. LightGBM can also internally handle categorical data without explicitly converting those to dummy variables. However, the analysis requested to look into the various channels and campaigns about how these are affecting the target. Hence, I have explicitly created dummy varieables for specifically those variables: channel_id & utm_campaign

I have chosen accuracy and Area Under the Curve (AUC) as two metrics. AUC is a much better choice here becausw we are dealing with a highly imbalanced dataset with too many negative cases. An f-score can also be used, depending on whether False Positives or False Negatives are more detrimental for the predictions.

Budget is an important consideration for these campaigns, which is unkown. 

I would also like to test different attribution models using historical data or A/B testing to evaluate their performance and accuracy. Eventually, comparing the results across models and choosing the one that best meets the objectives and providing actionable insights.

I can also learn how to get better quality data with fewer missing data and more data across time. Typically, I would like to divide the data by season, geography, and other demograpics to gain deeper insights. 


* [Full Noebook](https://github.com/agniji/DO_Campaigns/blob/main/AttribModel.ipynb)

