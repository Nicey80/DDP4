---
title       : Campaign Planner
subtitle    : Tracking Marketing Campaigns through Shiny
author      : Paul Nice
job         : 
framework   : io2012      # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
--- 

<style>
em {
  font-style: italic
}
.title-slide {
    background: url('assets/img/FirstScreen.GIF') no-repeat;
    background-size: 600px 350px;
    background-position: 90% 10%;
    <!-- background-color: #FFFFFF; /* #EDE0CF; ; #CA9F9D*/ -->
}
.r {
    font-size: 10px
}

</style>




## App Overview

Prototype Campaign Planning Tool can be found at <br>
http://35.176.36.56:3838/CampaignPlanner/
<br>
### Target Audience
The App is intended to be used by a team of people responsible for 
creating marketing campaigns.

### Usage
The App is intended to track changes to the
plan in terms of launch dates, response rates, product conversions etc.

Using the App it is also possible to scenario plan for changes to the plan to 
see the impact on the key metrics



--- 
## Key Components


### Plan Summary
- Houses the live plan
- Allows the user to easily modify the current plan. Send Dates, Response Rates, Conversion Rates
- Visualise the impact of the changes and convert into a scenario if required

### Scenario Planning

- Allows the user to compare in graph or table form the relative impacts of multiple scenarios
- Allows the user to create new scenarios based on the existing plans



---

## Sample Code


```r
library(readxl)
library(tidyverse)

DT1 <- read_excel("InitCampDB.xlsx", sheet=1)
DT2 <- read_excel("InitCampDB.xlsx", sheet=2)

DT <- left_join(DT1, DT2, by="ForecastID")

DT <- DT %>%
    group_by(ForecastID) %>%
    summarise(Total_Vol = sum(`Batch Vol`))

p <- ggplot(DT)+
    geom_col(aes(ForecastID, Total_Vol, fill=as.factor(ForecastID)))

p+ggtitle("Total Send Volume per scenario")
```

![plot of chunk unnamed-chunk-1](assets/fig/unnamed-chunk-1-1.png)



---

## Proposed Future Development

Additional Future Development is planned to cover the followinf areas
- Approval Workflow. *Create an approvals workflow so necessary approvers can review and approve teh impact of any changes*
- Campaign Reporting. *Bring in feed from reporting systems to measure campaign effectiveness*
- Live Reforecasting. *Using the actual data fed from the reporting system undertake an automated reforecast of the live plan*
- Global Plan. *Integrate Forecasting of non campaign elements using the campaign data and other sources of information to inform the forecasts*
- Global Sales Plan. *Maintain a live view of the Global Sales Plan including feeds from other Sales Channels* 
