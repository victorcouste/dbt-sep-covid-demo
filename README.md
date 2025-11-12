# dbt-sep-covid-demo

SEP means Starburst Enterprise Platform, the on-premises or self-managed Starburst product.
Inspired by the https://github.com/dbt-labs/dbt-starburst-demo repo using Starburst Galaxy (SaaS, fully-managed Starburst product).

## What you'll need:

- A [Starburst Enterprise cluster](https://www.starburst.io/starburst-enterprise/).
- A AWS account with S3 bucket
- A dbt Core installation of your choosing or a [dbt Cloud account](https://www.getdbt.com/fr/free-account). For dbt Core I used a virtual environment on my M1 mac because that was the most recommended. I'll add the steps below in this readme. Review the other [dbt core installation information](https://docs.getdbt.com/dbt-cli/install/overview) to pick what works best for you.
- A PostgreSQL database

Ask me Covid datasets to be integrated into your AWS S3 bucket and your PostgreSQL database.

Why are we using so many data sources? Well, for this data lakehouse tutorial we will take you through all the steps of creating a reporting structure, including the steps to get your sources into your land layer in S3. Starburst solutions superpower with dbt is being able to federate data from multiple different sources into one dbt repository. Showing multiple sources helps demonstrate this use case in addition to the data lakehouse use case. If you are interested in only using S3, you can run all the `TPCH` and `AWS` models without having to create a snowflake login. The PostgreSQL section will fail, but the rest should complete.

### Tutorial Information

The goal of this tutorial is to showcase the power of dbt + Starburst Enterprise. This tutorial aims to demonstrate both superpowers.

1. Query federation across multiple data sources - dbt specializes as a transform tool and can only be utilized after the data is landed in a storage solution. Starburst Enterprise fixes that by allowing you to query your data from multiple sources.
2. Data Lakehouse analytics - In this lab, we are going to build our lakehouse reporting structure in S3 and use slightly different naming conventions from the traditional Land, Structure, and Consume layer to accomodate for dbt standards. Land = Stage, Structure = Intermediate, Consume = Aggregate. For more information about the Starburst data lakehouse, visit this [blog](https://www.starburst.io/blog/part-2-of-current-data-patterns-blog-series-data-lakehouse/).


Visit this [blog](https://www.starburst.io/blog/build-a-data-lakehouse-reporting-structure-with-dbt-and-starburst-galaxy/) for more information on the tutorial (using Starburst Galaxy product).

## The demo itself

### Installing dbt in your local environment

1. Install the `dbt-trino` adapter plugin, which allows you to use dbt together with Trino / Starburst Enterprise. You may want to do this inside a Python virtual environment. Below I list the steps I took to create my virtual environment.

```sh
python3 -m venv dbt-env
```

```sh
source dbt-env/bin/activate
```

```sh
pip install --upgrade pip wheel setuptools
```

```sh
pip install dbt-trino
```

Make sure you are up to date on your versions.

```sh
dbt --version
```

Other helpful links to getting started with setting up your virtual environment:

- [Install with pip](https://docs.getdbt.com/docs/get-started/pip-install) dbt instructions
- [Starburst documentation](https://docs.starburst.io/data-consumer/clients/dbt.html) which dives into more detail about the process described above
- [Python download](https://www.python.org/downloads/)

### Getting Started with this repository

1. Clone this GitHub repo to your local machine: `git clone https://github.com/monimiller/dbt-sep-covid-demo.git`

2. Copy `sample.profiles.yml` to the root of your machine, `~/dbt/profiles.yml`. (Why? This file will contain your `password` for connecting to Trino/Starburst, so you don't want it checked into `git`.)

```
cp ./sample.profiles.yml ~/.dbt/profiles.yml
```

4. Open the file, and update the fields denoted by `<>` with your own user, password, cluster, catalog an schema (Specify a Starburst Iceberg type catalog if you want to create Iceberg tables).

5. Verify that you can connect to Trino / Starburst Enterprise.

```
dbt debug
```

6. Install dbt packages ([`dbt_utils`](https://hub.getdbt.com/dbt-labs/dbt_utils/latest/)) for use in the project:

```
dbt deps
```

7. Try running dbt:

```
dbt run
dbt test
dbt build
```

8. Generate and view documentation:

```
dbt docs generate
dbt docs serve
```


## More on dbt + Trino

Watch recordings from past Trino community broadcasts:

- <https://trino.io/episodes/21.html>
- <https://trino.io/episodes/30.html>
