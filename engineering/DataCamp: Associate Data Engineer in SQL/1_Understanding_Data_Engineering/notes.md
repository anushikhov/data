# Understanding Data Engineering

> What is data engineering?
> Stroing data
> Moving and processing data

## Responsibilities:
**Data Engineer:** data collection and storage
**Data Analyst:** data preparation
**Data Scientist:** exploration and visualization
**ML Engineer:** experimentation and prediction

## Data engineers deliver:
* the correct data
* in the right form
* to the right people
* as efficiently as possible

## A data engineer's responsibilities:
* ingest data from different sources
* optimize databases for analysis
* remove corrupted data
* develop, construct, test & maintain data atchitectures

## In order of volume big data is mainly composed of:
* sensors and devices data
* social media data
* enterprise data
* VoIP data

## The five Vs of Big Data
* **Volume** (how much? the quantity of data points)
* **Variety** (what kind? the type and nature of the data)
* **Velocity** (how frequent? how fast is the data generated and processed)
* **Veracity** (how accurate? how trustworthy the sources are)
* **Value** (how useful? how actionable the data is)

| Data Engineer           | Data Scientist           | 
| ----------------------- | -------------------------|
| ingest and store data   | exploit data             |
| set up databases        | access databases         |
| build data pipelines    | use pipeline outputs     |
| strong software skills  | strong analytical skills |

**Data pipelines ensure efficient flow of the data.**

## Data pipelines help:
| Automate                 | Reduce                     |
| -------------------------| -------------------------- |
| extracting               | human intervention         |
| transforming             | errors                     |
| combining                | time it takes data to flow |
| validating               |                            |
| loading                  |                            |

**ETL is a popular framework for designing data pipelines.**
1. Extract data
2. Transform the extracted data
3. Load the transformed data to another database

## Data pipelines
* move data from one system to another
* may follow ETL but not always
* data may not be transformed
* data may be directly loaded in applications

-----------------------------------------------------------------------------

* Structured data
* Semi-structured data
* Unstructured data


|  Data Lake                          |  Data warehouse                     |
|-------------------------------------|-------------------------------------|
| Stores all the raw data             | Specific data for specific use      |
| Can be petabytes (1 million GBs)    | Relatively small                    |
| Stores all data structures          | Stores mainly structured data       |
| Cost-effective                      | More costly to update               |
| Difficult to analyze                | Optimized for data anlysis          |
| Requires an up-to-date data catalog |                                     |
| Used by data scientists             | Also used by data/business analysts |
| Big data, real-time analytics       | Ad-hoc, read-only queries           |


## Data catalog for data lakes:
* What is the source of the data?
* Where is the data used?
* Who is the owner of the data?
* How often is the data updated?
* Good practice in terms of data governance 
* Ensures reproducibility

**No data catalog -> data swamp**


