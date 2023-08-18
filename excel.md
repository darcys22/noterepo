## Number Fomatting

### Standard Currency with decimals
```
_($* #,##0.00_);_($* (#,##0.00);_($* "-"??_);_(@_)
```

### Standard Currency rounded to dollar
```
_($* #,##0_);_($* (#,##0);_($* "-"??_);_(@_)
```

### Standard Currency rounded to thousands
```
_($* #,##0,_);_($* (#,##0,);_($* "-"??_);_(@_)
```

## Balance Checking

Will check if zero, if true it prints OK!
```
_(* #,##0.000_);_(* (#,##0.000);"OK!";"ERROR"
```

## Dates

Formula to get financial year
```
Previous Year: =DATE(YEAR(Year_Cell)-1,MONTH(Year_Cell),DAY(Year_Cell)) 
Next Year: =DATE(YEAR(Year_Cell)+1,MONTH(Year_Cell),DAY(Year_Cell)) 
```

Take a date and return the FY
```
=IF(MONTH(Date_Cell)<6,YEAR(Date_Cell),YEAR(Date_Cell)+1)
```

Formatting
```
dd mmmm yyyy
```
