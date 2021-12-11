# James Muehlemann - Project 1 
## 10.30.21
### Project Overview
In this project, I was tasked with loading millions of rows of data to an Elasticsearch instance and then analyzing this data using Kibana. I was able to do this using:
- Docker Containerization
- Python 
- Elasticsearch
- Kibana
- AWS EC2 Instance Provisioned with Ubuntu

For this project we used [NYC Open Data][NYCOD] to digest and analyze millions of rows of parking data using the [Open Parking and Camera Violations(OPCV)][OPCV] API and the [Socrata Open Data API][SOC]. The Socrata API allowed me to build a command line interface using Python to connect to the OPCV API and query the data. 

### File Hierarchy
| File/Directory | Description |
| ------ | ------ |
| project01  | Root Project Folder |
|+ -- Dockerfile | Dockerfile to build the Docker image |
| + -- requirements.txt | Additional packages needed to run main.py |
| + --  src/ | Folder housing main.py |
| + --  + -- main.py | Python Script to query data and upload to ES |
| + -- assets/ | Folder housing Kibana Dashboard |
| + -- + -- kibana_dashboard.png | Dashboard of Parking Visualizations|
|+ -- README | README discussing details of the project | 

### Decision Making
For this project I had to make a few decisions in terms of field selection, page size, number of pages, and how I wanted to upload the data to Elasticsearch. I decided to query 15 of the fields available and use several of them for my visualizations. I chose issue_date as my time field. For page size I chose 10,000 rows over 20 pages, querying about 200,000 rows an upload. By using the Bulk API I was able to query more than 12,000,000 rows of parking violation data and then visualize this data using Kibana. 

### Steps to run Docker
#### Step 1: Build the Docker image
```sh
docker build -t bigdata1:1.0 project01/
```
#### Step 2: Access the project01/ directory
```sh
cd project01/
```
#### Step 3: Specify the parameters and run the Docker image 
```sh
docker run -v $PWD:/app -e DATASET_ID="nc67-uf89" -e APP_TOKEN="ENTER_APP_TOKEN" -e ES_HOST="https://search-sta9760james-t4ooyfa3fw3cqyathuuggj4gdi.us-east-1.es.amazonaws.com" -e INDEX_NAME="parking_violations" -e ES_USERNAME="ENTER_USERNAME" -e ES_PASSWORD="ENTER_PASSWORD" bigdata1:1.0 --page_size=3 --num_pages=2
```


[NYCOD]: <https://opendata.cityofnewyork.us/>
[SOC]: <https://dev.socrata.com/>
[OPCV]: <https://dev.socrata.com/foundry/data.cityofnewyork.us/nc67-uf89>