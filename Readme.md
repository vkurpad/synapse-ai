# Synapse Cognitive Pipelines

Synapse cognitive pipelines infuses AI into Synapse pipelines to extract latent structure and make predictions on unstructured or structuredd data. With cognitive pipelines you can add AI to automate tasks like form processing by extracting form contents for automation or analysis. 

## Customer Feedback Analysis
Mining customer feedback is a common challenge for a number of organiations. In this example you can deploy a pipeline to take customer reviews and run it through a process of:

1. Identifying the language of the review
2. Translating all reviews from different languages to English
3. Mining the review for aspect level sentiment
4. Identfying entities
5. Identifying key phrases in each of the review

All of this information is then saved to SQL database in Synapse, where simple SQL queries can now answer questions like which aspect of a customer engagement had the loweest sentiment and what were the ey phrases associated with those reviews?

As a sample dataset, you can use the [hotel reviews dataset from Kaggle](https://www.kaggle.com/datafiniti/hotel-reviews). 

## Getting Sarted

To get started deploy the [Customer Feedback Analysis](https://web.azuresynapse.net/) pipeline from the Synapse knowledge center. 

### Assets Required

The cognitive pipeline uses Azure Cognitive Services to extract insights. You will need to provision a [Cognitive Services resource](https://docs.microsoft.com/en-us/azure/cognitive-services/text-analytics/overview).

Download the hotels review dataset or adapt the pipeline to work with your data. As an example here is a [sample dataset of a few hotel reviews](https://confdemo.blob.core.windows.net/hotel-reviews-small/HotelReviews_Free%20(1).csv?sv=2019-02-02&st=2020-12-03T05%3A16%3A00Z&se=2021-12-04T05%3A16%3A00Z&sr=b&sp=r&sig=CR92EPkfGt8u0B%2FUwcRVIHHO0FHrb%2Fe3zEHgSP5ItqI%3D).

### Configuration

Once the cognitive services resource deployment completes, save the key and the region for the resorce. These will be parameters to your pipeline.

Configure a linked service for an Azure Data Lake service and add the sample reviews file to a container called `hotel-reviews` in a folder named `input`. The pipeline requies a few other sinks that are all folders in the same container.

Configure a Synapse SQL pool for where the putputs will be written. 

### Running the Pipeline

With the parameters configured and the linked services configured, you can now run the pipeline and will see the following tables in your Synapse SQL pool:

1. CFA_Reviews: Table containing each of the reviews 
2. CFA_Entities: Table containing all the entites identified from the different reviews
3. CFA_Reviews_Entities: Table containing the references to the specific entities associated with each review
4. CFA_KeyPhrases: Table containing the key phrases idnetified
5. CFA_Reviews_KeyPhrases: Table containing the references to the key phrases identified in each review
6. CFA_Review_Sentiment: Sentiment associated with the overall review
7. CFA_SentimentAspect: Aspect level sentiment associated to the entity in a review
8. CFA_Translated: All non english reviews translated to english


