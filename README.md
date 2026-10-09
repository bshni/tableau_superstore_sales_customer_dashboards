# Mini Project 03 – Central Superstore Tableau Dashboards

This is my part of our team's Tableau project on the Central Superstore data. I'm **Mohamed Ahmed Rashed Atia** ([@bshni](https://github.com/bshni)), and I worked on it with **Ahmed Mahmoud** ([@amx-20](https://github.com/amx-20)). My part was **sales in relation to the customer dimension**.

The full project (the final merged workbook and everyone else's work) lives in our team leader's repo, so if you want the complete picture go here:
👉 https://github.com/hamza0sama/Mini_Project_03

This repo only covers what I built.

---

## What's in here

```
My team's Contribution to the project/
├── Mohamed Rashed and Ahmed Mahmoud.twb     # my workbook
├── Mohamed Rashed and Ahmed Mahmoud.twbx    # packaged version (data included)
└── Mohamed Rashed and Ahmed Mahmoud .md     # my notes while building it
```

The rest of the folders (`database/`, `dataset/`, `icons/`, other teams' workbooks) come from the shared project. I didn't build the database, that was the team leader's work, I only connect to it.

## Data source

The workbook connects to a SQL Server database called `Mini_Project_02`, which our leader designed (staging → bronze → silver → gold). I'm using the gold layer:

- `FactSales`
- `dimCustomer`
- `dimDate`
- `dimLocation`
- `dimProduct`

I had built a similar data warehouse myself before this ([sql_data_warehouse_business_analytics](https://github.com/bshni/sql_data_warehouse_business_analytics)), but we agreed as a team to use our leader's database so everyone's work stays unified.

Our leader made the date a separate dimension instead of keeping it inside the fact table, so I used `dimDate` for all the time-based analysis.

I also had to join the `silver.encounters` table to get the Order ID, since it wasn't available anywhere in the gold layer and I needed it to count orders per customer.

## What I built

Two dashboards, both using the same layout.

### Sales Dashboard
- KPIs: Total Sales, Total Profit, Total Quantity (each with current year vs previous year and the % difference)
- Sales & Profit by customer **Segment**, which is interactive and filters the rest of the dashboard when you click a segment
- Weekly Trends chart

### Customer Dashboard
- KPIs: Customers, Sales per Customer, Quantity per Customer
- Customer Distribution (by number of orders per customer)
- Top Customers

Both dashboards have **Category** and **Sub-Category** filters, plus custom filter/clear-filter buttons (icons are in the `icons/` folder).

## Design choices

- Maximum of **4 colors** across everything, following the advice from Eng. Baraa ("Data with Baraa" on YouTube). It was my first Tableau project, so I followed his tutorial and only applied the parts relevant to my section.
- KPI titles and numbers react to the filters, they're not static.

## Things I ran into

- **Slow loading workbook:** Taqey and Saif's workbook took about a minute to open because the SQL Server name was typed wrong in the connection. I fixed it.
- **Wrong data type:** Tableau picked the wrong type for the `Region` column in `dimLocation`. This exists in the other workbooks too, so I told the team.
- **KPIs not reacting to filters:** my first fix was wrapping the calculations in `WINDOW_SUM`, which got the KPIs reacting but didn't work for distinct aggregations and the difference number still didn't update. I ended up using a separate sheet for the title/difference values instead, which solved it properly. The tutorial doesn't cover this, so I had to figure it out on my own.

## How to open it

1. Download this repo.
2. Open the `.twbx` file in Tableau, since it has the data packaged inside and works without a database connection.
3. If you use the `.twb` instead, you'll need SQL Server running with the `Mini_Project_02` database (script is in the team repo linked above) and you'll have to update the server name in the connection to match yours.

## Credits

The team behind the full project:

- **Hamza** (team leader) – database design and the final merged project: [@hamza0sama](https://github.com/hamza0sama)
- **Mohamed Ahmed Rashed Atia** (me) – sales by customer dashboards: [@bshni](https://github.com/bshni)
- **Ahmed Mahmoud** – worked with me on this part: [@amx-20](https://github.com/amx-20)
- **Saif elden khaled**: [@Saifeldenkhaled](https://github.com/Saifeldenkhaled)
- **Taqey**: [@Taqey](https://github.com/Taqey)
- **Mohamed abdalqader**: [@mo3abdalqader](https://github.com/mo3abdalqader)

Tutorial followed: **Data with Baraa** (Tableau project tutorial).
