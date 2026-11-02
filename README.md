# Name-Screening-PBI

Outstanding_Age_Working_Days =
VAR CreatedDate =
    DATEVALUE(Fact_Outstanding[creation_date])

VAR ReportDate =
    DATEVALUE(Fact_Outstanding[ReportingAsOfDate])

RETURN
IF(
    ISBLANK(CreatedDate) ||
    ISBLANK(ReportDate) ||
    CreatedDate >= ReportDate,
    0,
    COUNTROWS(
        FILTER(
            CALENDAR(
                CreatedDate + 1,
                ReportDate
            ),
            WEEKDAY([Date], 2) <= 5
        )
    )
)


Pending_Age_Calendar_Days =
VAR CreatedDate =
    DATEVALUE(Fact_Outstanding[creation_date])

VAR ReportDate =
    DATEVALUE(Fact_Outstanding[ReportingAsOfDate])

RETURN
IF(
    ISBLANK(CreatedDate) ||
    ISBLANK(ReportDate) ||
    CreatedDate >= ReportDate,
    0,
    DATEDIFF(
        CreatedDate,
        ReportDate,
        DAY
    )
)
