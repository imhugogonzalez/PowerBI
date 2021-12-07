# Using SUMX to excluce weekend's sales
Left chart is using the default SUM measure to display the sales by date,
while the right chart is using a custom measure that sums all sales, excluding the weekends (i.e. Saturdays and Sundays).

<img src="files/SUMX_NoWeekends.PNG" alt="a" width="1080"/>


## Meausure used by the slider
```
noWeekends = DATEADD(
                    tblInternetSales[OrderDate], 
                      SWITCH(
                            WEEKDAY(
                                    tblInternetSales[OrderDate],2
                                    )
                            ,6,-1,7,-2,0
                            )
                    ,DAY
                    )
```


## Meausure used by chart
```
sumSalesNoWeekends = SUMX(
                          tblInternetSales,
                          switch(
                                  weekday(
                                          tblInternetSales[OrderDate],2
                                          ),
                                          6,0,7 ,0,tblInternetSales[SalesAmount]
                                  )
                          )
```
