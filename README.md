# Marketing-Campaign-and-ROI-Tracking-PowerBI-project

# MARKETING CAMPAIGN AND ROI TRACKING ANALYSIS:

**DOMAIN**-Marketing 

**FUNCTION**-ROI tracking, Budget allocation, Strategic planning

A marketing campaign is a coordinated set of activities designed to promote a product, service, or brand across multiple channels to achieve specific business goals—such as increasing awareness, driving conversions, or boosting revenue. 

Here, we had m

# DATASET

Here is the dataset provided.
https://docs.google.com/spreadsheets/d/13FtYuDTfyUYtUwWr1G_6zEPXV4OtL02o/edit?usp=sharing&ouid=107010945020711302175&rtpof=true&sd=true
This is the dataset of marketing campaign of few companies in the digital platform for the year 2021.

# SITUATION

**1. ROI Tracking -Situation-based Question:**

**Situation**

Over the last few months, our team has launched several marketing campaigns across different platforms—Email, Google Ads, Instagram, YouTube, and even through influencer partnerships. We've also targeted a wide range of customer segments, from Foodies and Fashionistas to Outdoor Adventurers and Tech Enthusiasts.

While the overall numbers look promising—revenue is coming in and ROI looks decent—there are still some lingering questions. Some campaigns seem to be working much better than others, and there's a growing concern that we might be spending too much on channels that aren't delivering enough value.

The marketing team wants to know:

"Which marketing channels, campaign types, and customer segments are generating the highest return on investment (ROI), and how can we optimize our marketing spend by reallocating resources toward the most profitable and engaging areas?"

**2. Budget Allocation – Situation-Based Question:**

**Situation**

Over the past year, the marketing team at a mid-to-large enterprise launched multiple digital campaigns across various channels — including Social Media, Search, Influencer collaborations, Display Ads, and Email — targeting audiences in multiple languages and geographies.

After heavy investments across Q1–Q4, leadership raised concerns about whether their spend was yielding optimal returns, especially with rising CPC rates and only moderate growth in customer acquisition.

Additionally, despite reaching over 220 million impressions, conversions and profit margins seemed uneven across channels, languages, and regions.

At the same time, some internal stakeholders observed anecdotal success in specific language-targeted campaigns and during seasonal peaks (like Q2 and Q4), prompting a deeper dive into ROI tracking and revenue attribution per campaign type.

The marketing analytics team wanted to know:

* Which campaign types are actually driving the most revenue and conversions?

* Are there specific languages or regions where our marketing resonates more?

* Is our cost-per-click (CPC) justifiable, and how does it vary by campaign?

* Should we continue investing evenly across channels, or refocus?

**3. Strategic planning- Situation-Based Question:**

**Situation**

Over the last few months, we’ve launched a range of marketing campaigns—across influencers, search ads, social media, email, and display—targeting various customer groups. While we’ve seen some good results overall, it's clear that some strategies are working better than others, and some audiences are responding more than others.

As we start planning for the next quarter, the team wants to be more focused and intentional. Instead of spreading our budget evenly, we need to identify what’s actually driving impact—and where we may be overspending without getting much in return. The goal is to make smarter choices about which campaigns to invest in and which audiences to prioritize, based on what’s truly working.

The marketing teams wants to know:

*  Are there specific marketing strategies that are outperforming others—and should we be reallocating budget based on what’s working best?

*  Are we targeting the right audience segments, or are we overspending on groups that aren't delivering value?
  
*  Are some of our marketing channels becoming less effective over time—and how should we respond? 

# TERMS AND DISCUSSION

Before starting, we must know few terms that are used in marketing campaign analysis:

* **ROI:** ROI stands for Return on Investment. ROI is a key performance metric used to evaluate how effective a marketing campaign (or any investment) is at generating profit relative to its cost.

**Formula:** ROI = (Revenue−Acquisition Cost)/Acquisition Cost × 100

* **Acquitision Cost:** Acquisition Cost refers to the total cost of acquiring a customer or lead through a marketing campaign.

In simple terms, it's how much money you had to spend to get one person to take a desired action — like signing up, downloading, or making a purchase.

**Formula:** Customer Acquisition Cost (CAC) = Total Campaign Cost/Number of Customers Acquired 

* **CPC:** CPC stands for Cost Per Click. It is a digital marketing metric that shows how much you pay every time someone clicks on your ad.

In Simple Terms, if you run an ad on Google, Facebook, Instagram, etc., and someone clicks on it, you are charged a certain amount—that amount is your CPC.
​
**Formula:** CPC = Total Number of Clicks/Total Cost of Campaign

* **Conversion Rate:** Conversion Rate tells you how many people took a desired action (like signing up, purchasing, or downloading) after clicking on your ad or visiting your site.

**Formula:** Conversion Rate = (Number of Conversions/Total Visitors or Clicks) × 100

* **​Engagement Score:** Engagement Score is a metric that shows how actively your audience is interacting with your content, ads, or campaigns. It combines several types of user behaviors — like clicks, likes, shares, comments, time spent — into a single score to measure overall interest and involvement.

**Formula:** Engagement Score = (Total Engagements/Total Impressions or Reach) × 100

# TASK:

1. Create the metrics
2. Create an end to end dashboard that helps the stakeholders to understand easily.
3. Create relevant insights that helpss in making data-informed decisions.

# BI Workflow: From Data Collection to Dashboard

# 1. Data Source:

--> Get Data  -->  Marketing platform APIs (Google Ads, Facebook Ads, Mailchimp) with OAuth tokens 

*Alternative:
Historic marketing campaign exports from internal teams
Public datasets or Google Analytics sample data
Simulated streaming by chunked incremental data loading*


# Data Transformation in Python:

-->Transform the data --> Select the csv file and expand it --> Check the data types -->  Check the null and missing values --> Check the duplicate values --> replace it --> cleaned data

**Apache Airflow**: Since the csv file consist of one dataset only, hence the required of apache airflow is not required.

# Build Metrics using DAX:

-> CALCULATED COLUMNS:

* profit = marketing_campaign_dataset[total_revenue_gained]-marketing_campaign_dataset[Acquisition_Cost]

* total_revenue_gained = marketing_campaign_dataset[ROI]*marketing_campaign_dataset[Acquisition_Cost]+marketing_campaign_dataset[Acquisition_Cost

* CPC = DIVIDE(marketing_campaign_dataset[Acquisition_Cost], marketing_campaign_dataset[Clicks])

* Estimated_Revenue = marketing_campaign_dataset[Conversion_Rate] * marketing_campaign_dataset[Acquisition_Cost]

--> CALCULATED MEASURES:

* Top_Campaign_Flag =  IF([ROI_Rank] = 1, "Top Performer", "Others")

* ROI_Rank = RANKX (ALL(marketing_campaign_dataset[Campaign_Type]),
    CALCULATE(AVERAGE(marketing_campaign_dataset[ROI])),,
    DESC,
    DENSE
)

# 4. Building the visuals and dashboard using PowerBI

**ROI Tracking:**
"![ROI Tracking](")

