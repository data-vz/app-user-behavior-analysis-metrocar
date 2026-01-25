# Metrocar: App User Behavior Analysis

## Business Context

Metrocar is a ride-hailing platform operating in a competitive market alongside established players such as Uber and Bolt. The platform enables users to download the mobile application, complete registration, request rides, travel to their destinations, process payments, and provide feedback on their experience.

Despite successful user acquisition through the app download funnel, the company faces a critical challenge: a significant portion of users fail to complete their first ride. This gap between registration and first ride completion represents substantial lost revenue and indicates potential friction points within the user journey. Understanding and addressing these barriers is essential for improving platform performance, maximizing return on marketing investment, and establishing a sustainable competitive position in the ride-hailing market.

## Project Objectives

The primary objectives of this analysis are to:

1. **Identify conversion bottlenecks** across the complete user journey, from initial app download through first ride completion
2. **Quantify user drop-off rates** at each stage of the funnel to prioritize optimization efforts
3. **Uncover root causes** of user attrition through data analysis and behavioral pattern identification
4. **Develop actionable recommendations** spanning product development, marketing strategy, and customer experience enhancement
5. **Establish optimization priorities** based on potential business impact and implementation feasibility

## Success Metrics

The effectiveness of this analysis and subsequent optimization initiatives will be measured through the following key performance indicators:

**Primary Metrics:**

- **Conversion Rate**: Percentage of app downloads that result in completed first rides, including intermediate conversion rates (download-to-signup, signup-to-ride-request, ride-request-to-completion)
- **Completed Rides Rate**: Ratio of requested rides that are successfully completed versus those abandoned or cancelled
- **Total Revenue**: Overall platform revenue generated, with particular focus on revenue impact from improved conversion

**Secondary Metrics:**

- **Number of Signed Users**: Total registered user base and registration completion rate
- **Customer Lifetime:** Average duration a user remains active with the service, from first to last interaction.
- **Average Rating**: User satisfaction score reflecting service quality and experience
- **Time to First Ride**: Duration between registration and first completed ride (velocity metric)
- **Drop-off Rate by Stage**: Specific abandonment rates at each funnel stage to identify critical intervention points

## Data and Methodology

### Data Sources

This analysis utilizes the Metrocar operational database, which captures comprehensive user interaction data across the entire customer journey (initial app download through signup, ride requests, completed rides, payment processing, and post-ride reviews). The database consists of five tables interconnected through key identifiers:

**User Journey Tables:**

- **app_downloads**: Records initial user acquisition, including app download key (unique session identifier), platform (iOS, Android, Web), and download timestamp
- **signups**: Contains user registration data with user ID, session ID linking to app downloads, signup timestamp, and demographic information (age range)
- **ride_requests**: Tracks all ride activity including ride ID, user ID, driver ID, request timestamp, acceptance timestamp, pickup/dropoff locations and timestamps, and cancellation timestamp where applicable

**Transaction and Feedback Tables:**

- **transactions**: Documents financial data with transaction ID, ride ID, purchase amount in USD, charge status, and transaction timestamp
- **reviews**: Stores post-ride feedback including review ID, ride ID, user ID, driver ID, numerical rating, and written review text

### Analytical Methodology

The analysis employs a multi-layered approach combining SQL-based data extraction and transformation with Tableau visualization to derive actionable insights:

**Funnel Analysis Framework:**
A comprehensive conversion funnel was constructed to map the complete user journey across eight critical stages: app download → signup → ride request → ride acceptance → pickup → ride completion → payment → review. SQL queries were developed to calculate stage-by-stage conversion rates, identify drop-off volumes and percentages at each transition point, and measure time intervals between funnel stages.

**Segmentation Analysis:**
User behavior patterns were systematically analyzed across two primary dimensions. Platform analysis compared performance and user engagement across iOS, Android, and Web interfaces to identify platform-specific friction points and optimization opportunities. Demographic analysis examined behavioral differences across age range segments to understand generational preferences and pain points.

**Performance Metrics:**
Key business metrics were calculated using SQL aggregations, including user lifetime value derived from requests data, time to first ride measuring onboarding efficiency, ride completion rates accounting for cancellations, and revenue metrics segmented by user cohorts and platforms.

**Visualization and Reporting:**
Tableau dashboards were developed to present findings through interactive funnel visualizations showing drop-off magnitude at each stage, trend analysis charts displaying segmentation comparisons highlighting platform and demographic differences.

### Limitations and Constraints

Several limitations should be considered when interpreting the analysis results:

**Temporal Constraints:**
The dataset represents a single time period (the year 2021) without historical comparison data, preventing longitudinal trend analysis and is deprived of seasonality assessment. 

**Analytical Scope:**
True cohort analysis tracking specific user groups over extended periods was not feasible with the available data structure. This limitation affects our understanding of user lifecycle patterns, prevents robust customer lifetime value projections, and constrains assessment of how user behavior evolves with platform tenure.

**External Factors:**
The analysis does not account for external variables that may influence user behavior, such as competitive market dynamics, seasonal demand fluctuations, regional economic conditions, or concurrent marketing campaigns. These uncontrolled factors may contribute to observed patterns but cannot be isolated within the current analytical framework.

Despite these limitations, the dataset provides sufficient granularity and coverage to identify critical conversion barriers, quantify their business impact, and develop evidence-based recommendations for platform optimization.

## Key Insights

### Business Performance Overview

Metrocar generated **$4,472,182 in total revenue** from **17,623 registered users**, resulting in an **average user lifetime value of $254**. 

User rating data reveals a concerning trend, with an **average platform rating of 3.06 out of 5**, suggesting significant room for service quality improvement. 

### Time to First Ride Distribution: Onboarding Efficiency Concerns

While the **modal time to first ride is one day**, indicating that many users successfully convert quickly, the distribution exhibits significant right-skew with some users taking **up to 362 days** to complete their first ride. This extreme variance shifts the **average time to first ride to 37 days**, suggesting substantial onboarding friction for a subset of users.

This pattern indicates two distinct user populations:

- **Fast converters**: Successfully navigate onboarding within 24 hours
- **Delayed converters**: Experience barriers that prevent immediate platform adoption

### Customer Lifetime

The platform maintains an **average customer lifetime of 60 days** across all platforms, indicating relatively short engagement periods that highlight the importance of maximizing early-stage conversion and retention.

### *Critical Conversion Barriers*

### Ride Completion Drop-off (-49%)

The most severe funnel leakage occurs between ride acceptance and ride completion, where only **64% of accepted ride requests convert to completed rides**. This represents a **49.23% user drop-off** at this critical stage and constitutes the single largest conversion barrier in the user journey.

**Root Cause Analysis - Driver Acceptance Delays:**

The primary driver of this drop-off is excessive waiting time before driver acceptance:

- **137,098 cancellations** occurred before driver acceptance, with an **average waiting time of 11 minutes**
- Waiting times **under 5 minutes result in zero cancellations**, establishing a critical service level threshold
- Waiting times of **5-10 minutes produce a 1.74% cancellation rate**, indicating the beginning of patience erosion
- Waiting times **exceeding 10 minutes result in 100% cancellation**, representing a complete failure point

**Post-Acceptance Cancellations:**

Even after driver acceptance, users continue to cancel if forced to wait an additional **21 minutes on average**. This suggests that acceptance alone does not resolve the service delivery issue, and total end-to-end fulfillment time remains problematic.

### Review Submission Drop-off (-30%)

The second major funnel leakage occurs between ride completion and review submission, with a **30.24% drop-off rate**. While less critical to immediate revenue, this gap limits feedback collection, reduces driver accountability mechanisms, and potentially impacts service quality improvement efforts.

**Demographic Patterns in Review Behavior:**

- **Lowest engagement**: Age ranges 18-24 and 45-54 show minimal review participation
- **Highest engagement**: Users aged 35-44 demonstrate the strongest propensity to leave reviews and represent the most active user segment for completed rides

### *Platform Performance Analysis*

### Revenue and User Distribution

**iOS emerges as the dominant platform**, generating **$71,447,000 in revenue** (approximately 71% of total revenue when extrapolating from the stated figures) and attracting the highest user volume. **Android** ranks second, followed by **Web** as the least utilized channel.

Despite this revenue disparity driven by user volume differences, platform performance metrics reveal remarkable consistency:

### Platform Parity in Key Metrics

All three platforms demonstrate **comparable performance** on core conversion and monetization metrics:

- **Average transaction amount**: Approximately **$20 across all platforms**
- **Download-to-completed-ride conversion rate**: Approximately **26% across all platforms**

This parity suggests that platform selection is primarily driven by user preference and market penetration rather than functional superiority. The iOS revenue advantage stems from higher user acquisition rather than better conversion efficiency, indicating that marketing and distribution strategies — not product experience — drive platform-level revenue differences.

## Strategic Implications and Recommendations

The platform performance uniformity has important implications:

- **Conversion barriers are platform-agnostic**, suggesting systemic issues in service delivery (driver availability, wait times) rather than interface design problems
- **Investment prioritization** should focus on operational improvements (driver supply, matching algorithms) that benefit all platforms rather than platform-specific UX optimization:
    - Implement dynamic surge pricing mechanisms that activate before wait times exceed 5 minutes, incentivizing more drivers to come online during high-demand periods
    - Introduce shift-based driver incentives offering guaranteed minimum earnings for drivers who commit to specific high-demand time blocks
    - Implement a tiered acceptance system where ride requests automatically escalate to a wider driver radius after 3 minutes without acceptance
    - Introduce parallel matching that sends requests to multiple nearby drivers simultaneously when wait times approach 5 minutes
    - Reduce post-acceptance cancellations by implementing real-time ETA updates that automatically notify users of delays and revised pickup times
    - Implement "express" ride tier with guaranteed shorter wait times at premium pricing for time-sensitive users
    - Track and penalize drivers with consistently slow pickup times through acceptance rate adjustments
- **Android and Web represent untapped growth opportunities** where improved marketing and distribution could yield revenue gains without requiring product differentiation
- Additional recommendation: **push notification campaign for first ride activation** to reduce the 29.6% drop-off between signup and first ride request through proactive user engagement:
    - Immediate post-signup (within 1 hour)
    - 24-hour follow-up
    - 3-day re-engagement
    - 7-day last attempt

These insights collectively point to a platform facing operational challenges — particularly in driver supply and matching efficiency — that overshadow platform-specific or demographic factors. The 10-minute wait time threshold and post-acceptance delays represent clear, actionable targets for service improvement that would directly address the largest conversion barrier and potentially improve the moderate 3.06 rating.