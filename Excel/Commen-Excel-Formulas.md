# Common Excel Formulas

## Index-Match

## Get every *nth* row of data

*In general:*

`=OFFSET(<startPoint>,(ROW(A1)*n)-1,0)`

*Example (increment by 2):*

`=OFFSET($B$5,(ROW(A1)*2)-1,0)`

*Note:* `A1` is always the same to reference first row

