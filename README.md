# Power-BI
How I built Power BI from the ground up using Markview data I had to use Dax Formulas to build my Report

The two formulas for CAPEX % & OPEX% show the percentage of each employee/contractor for each responsible director and visually observing trends. 
Capex % = [cost for Capex]/[Total Costs]
cost for Capex = CALCULATE(SUM('Dapitv'[cost]), 'Dapitv'[Cost Category] IN { "Capex" })
cost for Opex = CALCULATE(SUM('Dapitv'[cost]), 'Dapitv'[Cost Category] IN { "Opex" })
Hours in Daptiv = CALCULATE(SUM('Dapitv'[Hours Worked]))

Opex % = [cost for Opex]/[Total Costs]
Total Costs = SUM(Dapitv[cost])
Varience in Hours = Table2[Hours Forecasted] - Dapitv[Hours in Daptiv]
Hours Forecasted = CALCULATE(SUM('Table2'[Hours]))


Date = 
VAR MinYear = YEAR(MIN(Daptiv[Work Date]))
VAR MaxYear = YEAR(MAX(Daptiv[Work Date]))
RETURN
ADDCOLUMNS(
    FILTER(
        CALENDARAUTO(),
        AND(YEAR([Date]) >= MinYear, YEAR([Date]) <= MaxYear)
    ),
    "Calendar Year", "CY" & YEAR([Date]),
    "Year", YEAR([Date]),
    "Month Name", FORMAT([Date], "mmmm"),
    "Month Number", MONTH([Date]),
    "Weekday",FORMAT([Date], "dddd"),
    "Weekday Number", WEEKDAY([Date]),
    "Quarter", "Qtr" & TRUNC((MONTH([Date])-1)/3)+1
)
