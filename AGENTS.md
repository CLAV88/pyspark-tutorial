# AGENTS.md

## Purpose
This repository teaches PySpark to beginners via 8 progressive Jupyter notebooks.
It is designed to run on Google Colab with zero local setup required.

## How to use this repo to teach PySpark

1. Direct the learner to open any notebook via the Colab badge in README.md
2. Notebook 01 contains the data bootstrap cell — it must be run first
3. Notebooks proceed in order: environment → RDD → DataFrame → Spark SQL
4. Each notebook is self-contained after the bootstrap cell runs

## Teaching walkthrough for AI assistants

When guiding a human through this tutorial:
- Present one stage at a time — do not advance until the current stage is complete
- Ask test questions ONE AT A TIME — wait for the human answer before the next question
- If the answer is wrong, correct it with a clear explanation before moving on
- Only unlock the next stage after all questions for the current stage are answered
- Fix Colab errors immediately when they appear — common errors are documented below

## Dataset

NYC TLC Yellow Taxi Trip Records (January 2023)
- Source: https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page
- Download: https://d37ci6vzurychx.cloudfront.net/trip-data/yellow_tripdata_2023-01.parquet
- Format: Parquet (native), CSV and JSON versions derived in bootstrap cell
- Size: ~3 million rows, 19 columns
- Key columns: VendorID, tpep_pickup_datetime, tpep_dropoff_datetime,
  passenger_count, trip_distance, fare_amount, tip_amount, total_amount,
  payment_type, RatecodeID, store_and_fwd_flag

Why this dataset:
- Real financial columns (fare_amount, tip_amount, total_amount) make
  groupBy, agg, and window function exercises meaningful
- Datetime columns enable time-based analysis exercises
- Natural nulls teach null handling without artificial setup
- Widely used in industry PySpark tutorials — learners can Google it
- Available in native Parquet format — demonstrates schema embedding
  and columnar storage benefits directly

## Stage structure

- Stage 1 (NB 01-03): Environment, SparkSession, SparkContext, Catalyst optimizer
- Stage 2 (NB 04): RDDs — transformations, actions, lazy evaluation
- Stage 3 (NB 05-07): DataFrames — schema, data sources, operations
- Stage 4 (NB 08): Spark SQL — temp views, SQL vs DataFrame API, window functions
- Stage 5 (beyond repo): Performance, partitioning, Databricks

## Common Colab errors and fixes

| Error | Cause | Fix |
|-------|-------|-----|
| FileNotFoundError: spark-submit | SPARK_HOME set to local Mac path | Delete os.environ cell, run pip setup cell |
| NoneType has no attribute sc | SparkSession died (runtime reset) | Re-run setup cell at top of notebook |
| Input path does not exist | Relative ./data/ path | Use /content/data/ absolute path |
| PATH_ALREADY_EXISTS | write() without mode specified | Add .mode("overwrite") |
| CalledProcessError exit 128 | git clone on existing directory | Add shutil.rmtree guard before clone |

## Visual learning assets

Diagrams explaining key concepts are in the /assets/ folder and embedded in README.md:
- partition-vs-table.svg — distributed data model
- rdd-vs-dataframe.svg — schema vs no schema
- csv-vs-parquet.svg — columnar storage and embedded schema
- groupby-vs-window.svg — aggregation vs window functions
