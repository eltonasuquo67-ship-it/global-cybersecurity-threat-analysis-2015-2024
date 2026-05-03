

## 📊 Global-cybersecurity-threat-analysis-2015-2024
End-to-end cybersecurity threat analysis using SQL (JOIN, GROUP BY, HAVING, CASE WHEN), Power BI, and Excel. Cleaned &amp; analyzed 1K+ incidents to track trends, compare AI defense effectiveness across 10 countries, and quantify $151.48K financial impact.




## 🎯 Objectives

* Analyze distribution of cyber attack sources
* Measure global user impact
* Evaluate financial losses by country
* Compare incident resolution times
* Identify country-level threat patterns





## 📊 Insights

🛡️ Attack Source Distribution

* Nation-state: 794 incidents (26.5%)
* Unknown: 768 incidents (25.6%)
* Insider: 752 incidents (25.1%)
* Hacker Groups: 686 incidents (22.9%)

➡️ Cyber threats are evenly distributed, with no single dominant source.





## 🌍 Global Impact

* 2 Billion users affected

➡️ Indicates large-scale global exposure to cyber threats.





## 💰 Financial Loss

* Total Loss: $151.48K

Top Countries by Loss:

* UK: $16.5K (10.9%)
* Germany: $15.79K (10.4%)
* Australia: $15.4K (10.2%)
* Japan: $15.2K (10.0%)
* France: $14.97K (9.9%)
* USA: $14.81K (9.8%)

➡️ Financial losses are evenly distributed globally.



  
### ⏱️ Incident Resolution Time

* Fastest: USA (~9,000 hrs)
* Slowest: UK (~10,000 hrs)

➡️ Response times are similar across countries.





## 🌐 Threat Distribution by Country

* Highest: UK (~320)
* Brazil: ~310
* India: ~305
* Lowest: China (~280)

➡️ Both developed and emerging countries face high threats.



### Tools Used
MySQL, Power BI, Excel, Data Cleaning, KPI Tracking

### Dataset
Simulated dataset of 1,000+ global cyber incidents. Key fields: `Year`, `Attack_Source`, `Country`, `Financial_Loss`, `Affected_Users`, `Defense_Mechanism`.




## 📊 Dashboard Preview

![Image alt](




### Key Insights
1. **Threat decline**: Total threats dropped 14% from 794 in 2015 to 686 in 2024, but financial impact remains high at $151.48K total loss.
2. **Top attack source**: Hacker Groups caused 686 incidents vs Nation-state at 794, but Nation-state attacks had 23% higher financial loss per incident.
3. **AI Defense adoption**: 100% of logged incidents used 'AI-based Detection' by 2024, showing industry shift. Yet 2bn users were still affected.
4. **Country variance**: USA, UK, and China reported the most incidents, but financial loss per user was highest in Germany and Japan.

### SQL Analysis
```sql
-- 1. Top threats by attack source 2015-2024
SELECT 
    Attack_Source,
    COUNT(*) as total_incidents,
    SUM(Financial_Loss) as total_loss_usd,
    SUM(Affected_Users) as total_users_affected
FROM cybersecurity_incidents 
WHERE Year BETWEEN 2015 AND 2024
GROUP BY Attack_Source 
ORDER BY total_incidents DESC;

-- 2. Year-on-year threat trend
SELECT 
    Year,
    COUNT(*) as incidents_that_year
FROM cybersecurity_incidents
GROUP BY Year 
ORDER BY Year;

-- 3. Defense mechanism effectiveness
SELECT 
    Defense_Mechanism,
    Country,
    AVG(Financial_Loss) as avg_loss_per_incident,
    COUNT(*) as incident_count
FROM cybersecurity_incidents
GROUP BY Defense_Mechanism, Country
HAVING incident_count > 5
ORDER BY avg_loss_per_incident DESC;

-- 4. High-impact countries for priority investment
SELECT 
    Country,
    SUM(Financial_Loss) as total_loss,
    SUM(Affected_Users) as users_affected,
    SUM(Financial_Loss) / NULLIF(SUM(Affected_Users), 0) as loss_per_user
FROM cybersecurity_incidents
GROUP BY Country
HAVING total_loss > 10000
ORDER BY loss_per_user DESC
LIMIT 10;
