## Udacity Data Engineering Capstone Project

![](https://imgur.com/SrQms5c.png)


### Project Description

Amazon Customer Reviews is one of Amazon’s iconic products. In a period of over two decades since the first review in 1995, millions of Amazon customers have contributed over a hundred million reviews to express opinions and describe their experiences regarding products on the Amazon.com website. Specifically, this dataset was constructed to represent a sample of customer evaluations and opinions, variation in the perception of a product across geographical regions, and promotional intent or bias in reviews.

We build a data warehouse which analyze customre responses using data from 'books' categoreis in Amazon's reviews.

### Data sources

From [Amazon product Data](http://jmcauley.ucsd.edu/data/amazon/), we collect 2 data sources.

* **product reviews** : including reviews (ratings, text, helpfulness votes)

    ````json
    {
     "reviewerID": "A2SUAM1J3GNN3B",
     "asin": "0000013714",
     "reviewerName": "J. McDonald",
     "helpful": [2, 3],
     "reviewText": "I bought this for my husband who plays the piano.  He is having a wonderful time playing these old hymns.  The music  is at times hard to read because we think the book was published for singing from more than playing from.  Great purchase though!",
      "overall": 5.0,
     "summary": "Heavenly Highway Hymns",
     "unixReviewTime": 1252800000,
     "reviewTime": "09 13, 2009"
   }
   ````

* **metadata** : including product metadata(descriptions, category information, price, brand, and image features)

    ````json
    {
      "asin": "0000031852",
      "title": "Girls Ballet Tutu Zebra Hot Pink",
      "price": 3.17,
      "imUrl": "http://ecx.images-amazon.com/images/I/51fAmVkTbyL._SY300_.jpg",
      "related":
      {
        "also_bought": ["B00JHONN1S", "B002BZX8Z6", "B00D2K1M3O", "0000031909", "B00613WDTQ", "B00D0WDS9A", "B00D0GCI8S", "0000031895", "B003AVKOP2", "B003AVEU6G", "B003IEDM9Q", "B002R0FA24", "B00D23MC6W", "B00D2K0PA0", "B00538F5OK", "B00CEV86I6", "B002R0FABA", "B00D10CLVW", "B003AVNY6I", "B002GZGI4E", "B001T9NUFS", "B002R0F7FE", "B00E1YRI4C", "B008UBQZKU", "B00D103F8U", "B007R2RM8W"],
        "also_viewed": ["B002BZX8Z6", "B00JHONN1S", "B008F0SU0Y", "B00D23MC6W", "B00AFDOPDA", "B00E1YRI4C", "B002GZGI4E", "B003AVKOP2", "B00D9C1WBM", "B00CEV8366", "B00CEUX0D8", "B0079ME3KU", "B00CEUWY8K", "B004FOEEHC", "0000031895", "B00BC4GY9Y", "B003XRKA7A", "B00K18LKX2", "B00EM7KAG6", "B00AMQ17JA", "B00D9C32NI", "B002C3Y6WG", "B00JLL4L5Y", "B003AVNY6I", "B008UBQZKU", "B00D0WDS9A", "B00613WDTQ", "B00538F5OK", "B005C4Y4F6", "B004LHZ1NY", "B00CPHX76U", "B00CEUWUZC", "B00IJVASUE", "B00GOR07RE", "B00J2GTM0W", "B00JHNSNSM", "B003IEDM9Q", "B00CYBU84G", "B008VV8NSQ", "B00CYBULSO", "B00I2UHSZA", "B005F50FXC", "B007LCQI3S", "B00DP68AVW", "B009RXWNSI", "B003AVEU6G", "B00HSOJB9M", "B00EHAGZNA", "B0046W9T8C", "B00E79VW6Q", "B00D10CLVW", "B00B0AVO54", "B00E95LC8Q", "B00GOR92SO", "B007ZN5Y56", "B00AL2569W", "B00B608000", "B008F0SMUC", "B00BFXLZ8M"],
        "bought_together": ["B002BZX8Z6"]
      },
      "salesRank": {"Toys & Games": 211836},
      "brand": "Coxlures",
      "categories": [["Sports & Outdoors", "Other Sports", "Dance"]]
    }
    ````
### Data Schema

![](https://imgur.com/ivCE1lk.png)


### Run codes

The environment is made up of docker images.

````shell
docker-compose up -d
````


### Environment Configuration

  1. DataLake : Amazon S3 
  2. ETL Process : Spark (by Docker image)
  3. Data Warehouse : Postgresql-Cstore (by Docker image)

#### Senarios

  In the development environment, the Docker images are configured to operate on a single machine. However, when the volume of data grows, we can easily convert the ETL Process to Amazon EMR and the Postgresql-cstore to Amazon redshift. Redishift and amazon EMR, which perform distributed computing, can flexibly scale up and down to meet demand, so even more than 100+ people can handle it without problems.

In order to operate periodically(such as The pipelines would be run on a daily basis by 7 am every day) , you can convert the ETL pipeline currently written as a notebook file to airflow. 


