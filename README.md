# elastic_kibana_minio


Start Docker : docker-compose up

# basic crud 

# Check cluster heatlh
`GET _cluster/health`


# create index
`PUT employees`
# add data to employee
```
PUT employees/_doc/1
{
  "name" : "Mayank Raj" , 
  "age" : 23,
  "role" :  "software engineer"
}
```

# get mapping of index 
`GET employees/_mapping`


# builk insert 

```
POST _bulk
{ "index": { "_index": "employees", "_id": "21" } }
{ "name": "Alice Johnson", "age": 28, "salary": 75000, "role": "Software Engineer" }
{ "index": { "_index": "employees", "_id": "22" } }
{ "name": "Bob Smith", "age": 34, "salary": 92000, "role": "Project Manager" }
{ "index": { "_index": "employees", "_id": "23" } }
{ "name": "Charlie Brown", "age": 22, "salary": 60000, "role": "Data Analyst" }
{ "index": { "_index": "employees", "_id": "24" } }
{ "name": "David Wilson", "age": 40, "salary": 110000, "role": "CTO" }
{ "index": { "_index": "employees", "_id": "25" } }
{ "name": "Emma Davis", "age": 30, "salary": 85000, "role": "Marketing Manager" }
{ "index": { "_index": "employees", "_id": "6" } }
{ "name": "Frank Harris", "age": 27, "salary": 70000, "role": "DevOps Engineer" }
{ "index": { "_index": "employees", "_id": "7" } }
{ "name": "Grace Lee", "age": 32, "salary": 95000, "role": "HR Manager" }
{ "index": { "_index": "employees", "_id": "8" } }
{ "name": "Hank Green", "age": 29, "salary": 78000, "role": "Frontend Developer" }
{ "index": { "_index": "employees", "_id": "9" } }
{ "name": "Ivy Walker", "age": 25, "salary": 65000, "role": "UX Designer" }
{ "index": { "_index": "employees", "_id": "10" } }
{ "name": "Jack White", "age": 38, "salary": 105000, "role": "Product Manager" }
{ "index": { "_index": "employees", "_id": "11" } }
{ "name": "Katie Black", "age": 26, "salary": 72000, "role": "Backend Developer" }
{ "index": { "_index": "employees", "_id": "12" } }
{ "name": "Leo Adams", "age": 35, "salary": 99000, "role": "Solutions Architect" }
{ "index": { "_index": "employees", "_id": "13" } }
{ "name": "Mona Scott", "age": 31, "salary": 88000, "role": "Business Analyst" }
{ "index": { "_index": "employees", "_id": "14" } }
{ "name": "Nathan King", "age": 23, "salary": 63000, "role": "QA Engineer" }
{ "index": { "_index": "employees", "_id": "15" } }
{ "name": "Olivia Reed", "age": 37, "salary": 102000, "role": "VP of Engineering" }
{ "index": { "_index": "employees", "_id": "16" } }
{ "name": "Paul Young", "age": 28, "salary": 77000, "role": "Cybersecurity Analyst" }
{ "index": { "_index": "employees", "_id": "17" } }
{ "name": "Quincy Nelson", "age": 41, "salary": 115000, "role": "CFO" }
{ "index": { "_index": "employees", "_id": "18" } }
{ "name": "Rachel Scott", "age": 29, "salary": 79000, "role": "Scrum Master" }
{ "index": { "_index": "employees", "_id": "19" } }
{ "name": "Steve Martin", "age": 33, "salary": 94000, "role": "Database Administrator" }
{ "index": { "_index": "employees", "_id": "20" } }
{ "name": "Tina Brown", "age": 24, "salary": 68000, "role": "Machine Learning Engineer" }
```

# get data

`GET employees/_doc/3`

`GET employees/_search   //all data`



# filtering and querying
```
GET employees/_search
{
  "query": {
    "range": {
      "salary": {
        "gte": 60000,
        "lte": 80000
      }
    }
  }
}

GET employees/_search
{
  "query": {
    "match": {
      "name": "mayank"
    }
  }
}

```

# update document
```
POST employees/_update/1
{
  "doc" : {
    "role" : "Software Engineer"
  }
}
```

# delete document
`DELETE employees/_doc/{id}`

# delete whole index
`DELETE employees`



# Advance Search Pattern
```
GET employees/_search
{
  "query": {
    "match": {
      "role": "HR"
    }
  }
}

GET employees/_search
{
  "query": {
    "term": {
      "role.keyword": "HR Manager"
    }
  }
}

GET employees/_search
{
  "query": {
    "range": {
      "salary": {
        "gte": 70000,
        "lte": 80000
      }
    }
  }
}

```


# Advance Boolean Search Pattern
```
GET employees/_search
{
  "query": {
    "bool": {
      "must": [
        { "match": {"name": "mayank"}},
        { "match": {"age": 23}
        }
      ],
      "must_not": [
        {
          "match": {
            "salary": 45301
          }
        }
      ]
    }
  }
}

GET employees/_search
{
  "query": {
    "match_all": {}
  },
  "sort": [
    {
      "salary": {
        "order": "desc"
      }
    }
  ],
  "size": 100
}

```


# aggregations 
```
GET employees/_search
{
  "size": 0,
  "aggs": {
    "roleCount": {
      "terms": {
        "field": "role.keyword"
      }
    }
  }
}


GET employees/_search
{
  "size": 0, 
  "aggs": {
    "average salary": {
      "avg": {
        "field": "salary"
      }
    }
  }
}


GET employees/_search
{
  "size": 0, 
  "aggs": {
    "minimum_salary": {
      "min": {
        "field": "salary"
      }
    },
    "maximum_salary" : {
      "max": {
        "field": "salary"
      }
    }
  }
}

GET employees/_search
{
  "size": 0,
  "aggs": {
    "salary_ranges": {
      "histogram": {
        "field": "salary",
        "interval": 10000
      }
    }
  }
}

```




























