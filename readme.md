# Amplify Integration Batch Component

The Amplify Integration [**Batch Component**](https://docs.axway.com/bundle/amplify_integration/page/system_components.html) handles large datasets by partitioning them into smaller batches. This enables parallel processing, which improves overall throughput and reduces processing time. It also helps breaking down large updates to back end applications that may have update limitations. For example, an API or Database that has a limit on the number of records that can be written at a time.

As an added benefit, the Batch processor provides for reprocessing of failed records.

In this post, we'll review two use cases of the Batch component:

* Batch insert a large number of records to a database
* Reduce processing time required to publish a large of number of messages to Apache Kafka

An export of the Amplify Integration project can be downloaded from [**Github**](https://github.com/lbrenman/Amplify-Integration-Batch-Processing-Component)

## Batch Insert to a Database

In this use case, we'll use FileZilla to SFTP a CSV file of employees to Amplify Integration. The integration will parse the file and write the rows to a MongoDB Atlas database in batches as depicted below:

![Image](https://i.imgur.com/rKu0stH.png)

The integration without the Batch component is shown below:

![Image](https://i.imgur.com/Dg0AFAg.png)

As you can see from the MongoDB insert, Amplify Integration can insert all records at once:

![Image](https://i.imgur.com/A7jtF59.png)

However, what if your database can only handle a certain number of records (e.g. 1000) in a single insert. Then we can use the Batch processor component as shown below:

![Image](https://i.imgur.com/DcK8gsh.png)
![Image](https://i.imgur.com/pJ0jvmG.png)

If we review the transaction in the Monitor, we can see how a 4,998 row CSV file is split into 1,000 record simultaneous batches

![Image](https://i.imgur.com/Q5eknZC.png)
![Image](https://i.imgur.com/tjklrbt.png)

We can also see how clicking the Reprocess button on the Batch component provides the means to reprocess all records or just the failed records.

![Image](https://i.imgur.com/mBrS6J8.png)

For the 4,998 row CSV file, the non Batch version executed in 8.519 seconds. The Batch version executed in 10.72 seconds.

## Reduce Processing Time for Apache Kafa Publishing

In this use case, we'll use FileZilla to SFTP a CSV file of employees to Amplify Integration. The integration will parse the file and publish the rows to Apache Kafka (self hosted in AWS EC2) in distributed batches as depicted below:

![Image](https://i.imgur.com/p7E0JiM.png)

The integration without the Batch component is shown below:

![Image](https://i.imgur.com/qhIURtj.png)

In order to improves overall throughput and reduces processing time, we can use the Batch process component as follows:

![Image](https://i.imgur.com/QYR2his.png)
![Image](https://i.imgur.com/I0lYyH3.png)

For the 4,998 row CSV file, the non Batch version executed in 23:47.41 seconds. The Batch version executed in 9:47.212 seconds.