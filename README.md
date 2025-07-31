# Marketing-Campaign-and-ROI-Tracking-PowerBI-project

# MARKETING CAMPAIGN AND ROI TRACKING ANALYSIS:

**DOMAIN**-Marketing 

**FUNCTION**-ROI tracking, Budget allocation, Strategic planning

A marketing campaign is a coordinated set of activities designed to promote a product, service, or brand across multiple channels to achieve specific business goals—such as increasing awareness, driving conversions, or boosting revenue. 

In today’s competitive digital landscape, running marketing campaigns isn’t just about gaining visibility—it’s about driving measurable results. A well-structured marketing campaign aims to reach the right audience, convey the right message, and generate leads or sales efficiently. But how do we know if a campaign is truly successful? That’s where ROI (Return on Investment) tracking comes into play.

ROI tracking allows us to assess the performance of each marketing initiative by comparing the revenue generated to the cost of running the campaign. By monitoring key metrics such as acquisition cost, conversion rate, cost-per-click (CPC), and engagement, we gain actionable insights into what’s working, what needs optimization, and where to reallocate budget. This data-driven approach empowers marketers to make informed decisions, maximize returns, and continuously refine their strategies for better outcomes.


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

**1. ROI Tracking:**
![ROI Tracking](./Screenshot%202025-07-31%20083709.png)

* KPI: Sum of Acquisition Cost, Sum of Profit and Sum of Total revenue gained.
* Pie Chart for calculating the average of ROI vs Channel used
* Line Chart for Average of ROI by campaign type
* Metric table for Customer Segment, Sum of ROI and Average of engagement score.
* Slicer: Filter by Target Audience, Filter by Clicks and Company.


# Insights, Reasoning and Recommendations:

According to the 1st Situation that is ROI tracking where it was mentioned that:

The marketing team wants to know:

"Which marketing channels, campaign types, and customer segments are generating the highest return on investment (ROI), and how can we optimize our marketing spend by reallocating resources toward the most profitable and engaging areas?"

Based on that, I made the analysis and following results is found:

**What did we find?**

*Overall Financial Metrics:*

* Acquisition Cost: 2.49M

* Total Revenue Gained: 14.94M

* Profit: 12.5M
➤ The campaign is overall profitable, with a high ROI.

*Channel Performance (Pie Chart - Average ROI by Channel Used):*

**Top channels by ROI:**

* Email: 5.29

* Google Ads: 5.13

* Instagram: 5.07

**Lower ROI channels:**

* YouTube: 4.78

* Website: 4.95

-> All channels have similar share in usage (~16-17%).

*Campaign Type Performance (Line Chart - Average ROI by Campaign Type):*

**Top Campaign Types by ROI:**

* Display: ~5.4

* Social Media: ~5.3

* Search: ~5.1

**Low ROI Campaign Types:**

* Influencer Marketing: ~4.3

* Email: ~4.7

*Customer Segments (Metric Table):*

**Top Performing Segments (based on ROI and Engagement):**

Outdoor Adventurers: ROI = 222.25 | Engagement = 6.00

Foodies: ROI = 203.21 | Engagement = 5.54

**Lower Performing Segments:**

Health & Wellness: ROI = 183.18 | Engagement = 4.79

The overall campaign has been financially successful, generating a strong profit of ₹12.5 million from a total revenue of ₹14.94 million after spending ₹2.49 million on acquisition. When we look at how different marketing channels performed, Email, Google Ads, and Instagram delivered the highest returns on investment (ROI), while YouTube and Website channels showed lower returns. Interestingly, all channels were used almost equally, so the differences in ROI come from how effective each channel was rather than how much it was used.

In terms of campaign types, Display and Social Media campaigns stood out as the top performers, delivering higher ROI compared to other types. On the other hand, Influencer and Email campaigns showed lower ROI, meaning they were less efficient at turning investment into profit.

When it comes to customer segments, "Outdoor Adventurers" and "Foodies" responded the best to the campaigns, with the highest ROI and engagement scores. This means these groups were more interested and active, giving better returns for the money spent on them. In contrast, the "Health & Wellness" segment showed lower engagement and ROI, suggesting they were less responsive to the current campaign approach.

**Why is it happening?**

1. Influencer Marketing has the lowest ROI despite often being costly. This suggests:
* Possibly poor targeting or misalignment with the audience.
* Influencers used may not have strong conversion power.
* Campaigns may focus more on awareness than action.
  
2. Email performs well as a Channel but not as a Campaign Type, indicating:
* Email works best when used tactically rather than as the sole strategy.

3. Customer Segments with high engagement (e.g., Outdoor Adventurers, Fashionistas) are showing better ROI, likely due to:

* Better targeting and personalization.
* Products/services resonating well with their lifestyle and interests.

**What to do ?**

✅ Optimize Campaign Strategy: 

* Reduce spend on Influencer campaigns or focus on micro-influencers with higher engagement and niche audiences.
* Increase investment in Display and Social Media campaigns, as they deliver higher ROI.

✅ Refine Email Marketing:

* Use Email more tactically, such as:
* Retargeting warm leads.
* Abandoned cart recovery.
* Personalized product recommendations.
* A/B test subject lines and CTAs to boost email campaign effectiveness.

✅ Target High-Performing Segments: 

* Focus efforts on Outdoor Adventurers, Foodies, and Fashionistas with customized campaigns, since they show:
* Higher ROI.
* Strong engagement.

✅ Channel Mix Optimization: 

* Prioritize Email, Google Ads, and Instagram as high-performing channels.
* Re-evaluate YouTube and Website strategies to improve their ROI:
* Shorter, more actionable video content.
* Optimize landing pages for conversions.

✅ Engagement-Based Personalization:

* Use engagement scores to personalize messaging and offers.
* Higher engagement = higher ROI → use this to prioritize lead nurturing.
  

**Budget Allocation:**
![Budget Allocation](./Screenshot%202025-07-31%20083630.png)

* KPI: Sum of Impressions, Average of CPC, Average of Conversion rate.
* Silcers: Target Audience, Channel used and Company.
* Line chart for Average of total_revenue_gained by Quarter and Campaign type
* Area chart for Average of ROI by language
* Average of profit vs location.

  # Insights, Reasoning and Recommendation:

**What Did We Find?**

1. High ROI & Revenue Trends

* Influencer and Search campaigns show higher revenue growth in Q2 and Q4.
* The average ROI is slightly higher in German and Mandarin languages compared to others.
* Total impressions are high at 220M, indicating strong campaign reach.
* CPC (Cost per Click) is moderate at $32.20, with a conversion rate of 8% (decent industry average).

2. Location-Based Profit

* Profit is distributed across major U.S. regions, showing successful national reach.
* Some locations seem to contribute more significantly, likely due to regional responsiveness to specific campaigns.
* Language Impact
* Campaigns tailored in German and Mandarin are yielding higher ROI than those in English, French, or Spanish.

**Why Is This Happening?**

1. Language-Specific Content Resonance

* Non-English campaigns (especially in German and Mandarin) might be better localized or more culturally aligned, driving better engagement and conversions.

2. Seasonal Campaign Peaks
* Q2 and Q4 are typically high-activity quarters (summer promotions, holiday season), hence increased engagement and revenue.

3. Channel and Targeting Effectiveness
* Influencer and Search campaigns are likely more targeted, interactive, or personalized—leading to better performance and higher ROI.
* Social Media and Display ads may not be converting as well due to content fatigue or audience mismatch.

**What Should We Do?**

1. Double Down on What’s Working

Our Influencer and Search campaigns are clearly delivering better ROI, especially in Q2 and Q4. It makes sense to shift some of our budget away from lower-performing channels like Social Media and Display, and invest more in what’s actually working. Even a 20–30% reallocation can make a noticeable difference in returns.

2. Lean into High-ROI Languages

We're seeing better returns from German and Mandarin-speaking audiences. This tells us there’s real value in creating more targeted, localized content. Things like localized landing pages, native-language ads, and even regional offers could boost our results in these markets even further.

3. Fix or Pause What’s Not Performing

Email and Social Media campaigns haven’t been giving us great returns. Before we continue pouring money into them, let’s run a few A/B tests — maybe change up subject lines, images, timing, or CTAs — and see what’s actually resonating. If things still don’t improve, we should think about putting them on pause and redirecting the budget.

4. Target Regions That Are Already Winning

Certain regions in the U.S. are showing stronger profit levels. We should take advantage of this by launching geo-targeted campaigns tailored to those high-performing areas — think localized messaging or region-specific promotions.

5. Tweak Our CPC Strategy

Our average CPC is around $32.20, which isn’t bad — but there’s room for optimization. Let’s look at which keywords or placements are expensive but not converting well, and either bid lower or cut them altogether to free up budget.

6. Plan Ahead for Seasonal Peaks

ROI and revenue tend to spike in Q2 and Q4, so we should be prepping campaigns in advance for those quarters. That means locking in creative ideas, messaging, and offers early — so when those quarters hit, we’re not rushing, and we’re ready to perform.

**Strategic Planning**
![Strategic Planning](/Screenshot%202025-07-31%20084741.png)

* Metric table consist of Campaign type, Average of Acquisition Cost, Average of profit, Average of Conversion rate, ROI Rank, Top Campaign Flag, Average of CPC.
* Line chart for Sum of ROI by Campaign type and year
* Average of CPC by Target Audience.

# Insights, Reasoning and Recommendation:

**What Did We Find?**
* *Influencer Campaigns are Leading in ROI*
Even though all campaign types (like Email, Social Media, Display, and Search) have similar acquisition costs and conversion rates, Influencer campaigns are ranked highest in ROI. This suggests that influencer marketing is giving us the best value for the money spent right now.

* *Other Campaigns are Performing Similarly — but Less Efficiently*
Campaigns like Search, Email, Display, and Social Media are generating similar profits, but their ROI is slightly lower, so they’re not using our budget as effectively.

* *Cost Per Click (CPC) Varies by Audience*

Women aged 25–34 have the lowest CPC (about $31.88), meaning we’re spending less to reach and engage them.

Men aged 18–24 have the highest CPC (around $32.10), making them more expensive to target.

* *ROI Has Changed Over Time*

ROI from Influencer and Search campaigns increased, showing they’ve improved over time.

On the other hand, Email and Social Media ROI has declined, indicating these might not be working as well now.

**Why Is This Happening?**
* *Influencer Campaigns Are More Effective Right Now*
These campaigns may be better aligned with the audience. Influencers likely built trust with their followers, leading to stronger engagement and higher conversion.

* *Other Campaigns Are Getting Saturated or Outdated*
Channels like Email and Social Media may be experiencing ad fatigue, meaning customers are seeing the same type of content too often and are no longer engaging with it. Or, the targeting and messaging might not be as strong as before.

* *Some Target Audiences Are Cheaper to Reach*
Women aged 25–34 cost less per click, which means they’re either more interested, more engaged, or simply responding better to the ads.
Men 18–24 are more expensive, which could mean our messaging isn’t resonating with them as well.

**What Should We Do?**
1. Invest More in Influencer Campaigns.
Since these are performing best right now, we should:
Partner with more relevant influencers who match our brand and audience.
Make sure we track real results—not just likes or views, but actual conversions and profits.

2. Adjust Targeting Based on CPC.
Focus more of the budget on audiences like Women 25–34, who are cheaper and more responsive.
Reevaluate or improve the messaging for Men 18–24—or consider reducing spend on them if ROI doesn’t improve.

3. Refresh Email and Social Media Campaigns.
These channels are still useful, but they need a refresh:
Use personalized and creative content to recapture attention.
Try different formats (e.g., short videos, polls, quizzes).
Segment audiences better so they get more relevant messages.

4. Keep Tracking ROI Regularly.
What works now may change in a few months. So, we should:
Monitor ROI by campaign type and audience every month or quarter.
Use that data to update where we spend—and how we design campaigns.

# Conclusion

In today’s competitive landscape, tracking the ROI of marketing campaigns is not just helpful — it's essential. By understanding which campaigns drive actual results versus those that consume budget without returns, businesses can make smarter, data-backed decisions. In real-world scenarios, ROI tracking helps marketers identify top-performing channels, refine targeting strategies, and allocate budgets more efficiently. Ultimately, continuous monitoring and analysis of ROI ensures that every marketing dollar is spent with purpose, maximizing both impact and profitability over time.



