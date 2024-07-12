# Amplify Integration Batch Component

The Amplify Integration [**Batch Component**](https://docs.axway.com/bundle/amplify_integration/page/system_components.html) handles large datasets by partitioning them into smaller batches. This enables parallel processing, which improves overall throughput and reduces processing time. It also helps breaking down large updates to back end applications that may have update limitations. For example, an API or Database that has a limit on the number of records that can be written at a time.

In this post, we'll review two use cases of the Batch component:

* Batch insert a large number of records to a database
* Reduce processing time required to publish a large of number of messages to Apache Kafka

An export of the Amplify Integration project can be downloaded from [**Github**]()

## Batch Insert to a Database

In this use case, we'll use FileZilla to SFTP a CSV file of employees to Amplify Integration. The integration will parse the file and write the rows to a MongoDB Atlas database as depicted below:

![Image](https://i.imgur.com/rKu0stH.png)

## Reduce Processing Time for Apache Kafa Publishing