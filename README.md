# zillow-rapidapi-pipeline

This project goal was to successfully pull zillow data from RapidAPI and transform and loads this data into a table in Amazon Redshift. 
![airflow-graph](https://github.com/willtreuel6/zillow-rapidapi-pipeline/assets/79492506/83aabe9c-8dd7-490e-b872-6cf22f01abfe)

Throughout the pipeline we stay within the AWS Ecosystem, starting off by creating an EC2 instance and installing airflow onto the EC2 server.
![airflow-ec2](https://github.com/willtreuel6/zillow-rapidapi-pipeline/assets/79492506/88a4396b-b505-43b8-809e-7f0499c40ae8)

We then connect the EC2 instance to VSCode via SSH.
![vscode](https://github.com/willtreuel6/zillow-rapidapi-pipeline/assets/79492506/6c04eed3-d27f-40b2-aac6-ec7448ffc952)

Our first task is to load the raw JSON from RapidAPI into AWS S3 at a raw layer, we then trigger a lambda function that will make a copy of the raw data and load it into another S3 bucket that serves as a staging layer, again upon the copy landing in the S3 bucket it triggers another Lambda that will transform and model the data into a CSV file that is then placed into another S3 bucket. 
![buckets](https://github.com/willtreuel6/zillow-rapidapi-pipeline/assets/79492506/19be28c5-128d-4812-8d77-c889309c23c1)

Once our airflow instance kicks off the S3 loading jobs the next step is to use AWS S3 Sensor to see if there is a file that was dropped into our modeled CSV layer S3 bucket. If there was a drop there, then we will go onto our next task which is to load the data into AWS Redshift. 
Once the data has been loaded into our AWS Redshift Cluster we can go into the query editor and start to access the data we pulled and query it.

![redshift](https://github.com/willtreuel6/zillow-rapidapi-pipeline/assets/79492506/fa2869e8-2680-4bdb-868e-efa9a944bbed)
