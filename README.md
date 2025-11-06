# dbt + Trino: Starburst Galaxy COVID-19 tutorial!

There's a non-insignificant amount of setup work. The entire value prop of Trino and Galaxy is to be able to grab and transform data regardless of where it is. To demo this, you have to create at least one place for data to be and put data into it. Then you must set up a Galaxy account and give it access to the external data stores as well as where output data will be stored. The silver lining is that you only have to do this once, ever!

For the data source setup required for this tutorial, please see [INFRA_SETUP.MD](INFRA_SETUP.MD).


This demo can be utilized for either dbt Core or dbt Cloud. Both will require you to complete the steps in [INFRA_SETUP.MD](INFRA_SETUP.MD) to set up the appropriate data sources.

## What you'll need:

- A [Starburst Galaxy account](https://galaxy.starburst.io/login). This is the easiest way to get up and running with trino to see the power of trino + dbt.
- [AWS account to connect a catalog to S3](https://aws.amazon.com/free/?trk=78b916d7-7c94-4cab-98d9-0ce5e648dd5f&sc_channel=ps&s_kwcid=AL!4422!3!432339156165!e!!g!!aws%20account&ef_id=Cj0KCQjw166aBhDEARIsAMEyZh7cYVINX-G3ywOmeYJnSpMoRRr7xdxRScvE5qp5HqnDG0uTfIL_KFkaAtAGEALw_wcB:G:s&s_kwcid=AL!4422!3!432339156165!e!!g!!aws%20account&all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc&awsf.Free%20Tier%20Types=*all&awsf.Free%20Tier%20Categories=*all). AWS will act as a source and a target catalog in this example.
- Any snowflake login. [Sign up for a free account.](https://signup.snowflake.com/?utm_cta=trial-en-www-homepage-top-right-nav-ss-evg&_ga=2.209834001.529576585.1665973777-1488128661.1660321489) You don't need need snowflake for the demo, it would just require you to alter some models yourself.

Why are we using so many data sources? Well, for this data lakehouse tutorial we will take you through all the steps of creating a reporting structure, including the steps to get your sources into your land layer in S3. Starburst Galaxy's superpower with dbt is being able to federate data from multiple different sources into one dbt repository. Showing multiple sources helps demonstrate this use case in addition to the data lakehouse use case. If you are interested in only using S3, you can run all the `TPCH` and `AWS` models without having to create a snowflake login. The snowflake section will fail, but the rest should complete.

<img width="1588" alt="Screenshot-2023-05-05-at-10 11 05-AM" src="https://user-images.githubusercontent.com/33696269/236518678-0051088e-58b6-4f9e-b5c1-899e656cdfce.png">


You will also need:

- A dbt installation of your choosing (core or cloud).
- For **core**:  I used a virtual environment on my M1 mac because that was the most recommended. I'll add the steps below in this readme. Review the other [dbt core installation information](https://docs.getdbt.com/dbt-cli/install/overview) to pick what works best for you.
- For **Cloud**: I registered for a free account and utilized this repository in [dbt Cloud](https://www.getdbt.com/signup/). This option requires less first time setup steps. If you don't know what to pick, use this.

### Tutorial Information

The goal of this tutorial is to showcase the power of dbt + Starburst Galaxy together. This tutorial aims to demonstrate both superpowers.

1. Query federation across multiple data sources - dbt specializes as a transform tool and can only be utilized after the data is landed in a storage solution. Starburst Galaxy fixes that by allowing you to query your data from multiple sources.
2. Data Lakehouse analytics - In this lab, we are going to build our lakehouse reporting structure in S3 and use slightly different naming conventions from the traditional Land, Structure, and Consume layer to accomodate for dbt standards. Land = Stage, Structure = Intermediate, Consume = Aggregate. For more information about the Starburst data lakehouse, visit this [blog](https://www.starburst.io/blog/part-2-of-current-data-patterns-blog-series-data-lakehouse/).

### dbt Core
For the dbt Core tutorial, visit this [blog](https://www.starburst.io/blog/build-a-data-lakehouse-reporting-structure-with-dbt-and-starburst-galaxy/) for more information.
Use the [CORE.MD](https://github.com/monimiller/dbt-galaxy-covid-demo/blob/main/CORE.MD) as a README to run this demo using dbt Core.


### dbt Cloud
For the dbt Cloud tutorial, visit this [blog](https://www.starburst.io/blog/build-an-open-data-lake-architecture-with-dbt-cloud-and-starburst-galaxy/) for more information.
Use the [CLOUD.MD](https://github.com/monimiller/dbt-galaxy-covid-demo/blob/main/CLOUD.MD) as a README to run this demo using dbt Cloud.



### Shoutouts
Shout out to [@dataders](https://github.com/dataders) for his awesome help!
Inspired by the [Cinco de Trino](https://github.com/dbt-labs/trino-dbt-tpch-demo) repo by [@jtcohen6](https://github.com/jtcohen6)!
