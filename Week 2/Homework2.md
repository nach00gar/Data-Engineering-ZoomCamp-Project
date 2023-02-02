1) Just changing params to month=1, year=2020, color='green', rows: 447770

2) --cron "0 5 1 * *" 1st position is mm, 2nd is hh, 3rd is day, 4th month, 5th weekday

3) First, execute ex1 with provided months, then made the following changes to sum the total rows and parametrize
```
@flow()
def etl_gcs_to_bq(year, month, color):
    """Main ETL flow to load data into Big Query"""
    path = extract_from_gcs(color, year, month)
    df = transform(path)
    write_bq(df)
    return df.shape[0]

@flow(log_prints=True)
def etl_parent_flow(months: list[int] = [2, 3], year: int = 2019, color: str = "yellow"):
    total_rows=0
    for month in months:
        total_rows += etl_gcs_to_bq(year, month, color)
    print("Number of rows processed: "+str(total_rows)+"\n")
```
```
prefect deployment build -a ./etl_gcs_to_bq.py:etl_parent_flow -n "Ex3"
```

14851920

4) Created the code at github and the block at prefect.
```
prefect deployment build -a ./etl_web_to_gcs.py:etl_web_to_gcs -n "Ex4" -sb github/git --path "./Week 2/"
```

88605

5) Created the notification associated with the tag q5 I assigned to a new deployment and used the Slack Hook:

![image](https://user-images.githubusercontent.com/44344214/216469889-566a8a1a-a009-4516-be5a-55e7508d4d4f.png)


514392

6) Used the secret block to encode 0123456789, got ******** in the next UI page, then 8.
