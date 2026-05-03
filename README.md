#📊 Global-cybersecurity-threat-analysis-2015-2024
End-to-end cybersecurity threat analysis using SQL (JOIN, GROUP BY, HAVING, CASE WHEN), Power BI, and Excel. Cleaned &amp; analyzed 1K+ incidents to track trends, compare AI defense effectiveness across 10 countries, and quantify $151.48K financial impact.


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
