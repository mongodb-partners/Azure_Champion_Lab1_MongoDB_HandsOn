# Hands-on Tour of MongoDB Atlas

## Overview
MongoDB Atlas is a developer data platform integrating a multi-cloud database with a diverse set of data services. Atlas simplifies database deployment and management while enabling modern data-driven application development.

In this introductory-level lab, you will get hands-on practice with MongoDB Atlas. You will create your first forever-free cluster and set up App Services, including a GraphQL API. If you’re new to Atlas, you came to the right place! Read on to learn about this lab's specifics and areas you will get hands-on practice.

## Objectives
In this lab, you will do the following:
  - Provision your first MongoDB Atlas cluster
  - Create a database and collections with data
  - Set up App Services GraphQL API
  - Query data with the generated GraphQL API
  
 ## Prerequisites
 Since this lab is an introduction to MongoDB Atlas, you will need an Atlas account. You can register for MongoDB Atlas in one of two ways:
    1. Through the [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/mongodb.mongodb_atlas_self_serve_prod_2022?ocid=mongodb_iotmanufacturing_blog_FY23) if you have an Azure account. Refer to the [documentation](https://www.mongodb.com/docs/atlas/billing/azure-self-serve-marketplace/) to set up your subscription.
    2. With the [Atlas registration page](https://account.mongodb.com/account/register)
   
## Create an Atlas project and cluster
 In this section, you will get up and running, spinning up your first cluster and database.

### Provision a free cluster
Let’s deploy our first forever-free database in MongoDB Atlas! We’ll do that using the Atlas UI, so before starting, make sure you’re logged into your account.

  1. Click on the **Build a Database** button.
  
img1

  2. Click on the **advanced configuration options** link.
  
img2

  3. Select **Shared** and click **Create**.
  
img3

  4. Select a cloud provider and the region closest to your physical location.
  
img4

  5. Expand the **Cluster Name** section and rename your cluster to **Sandbox**.
  
img5

  6. Click **Create Cluster** to deploy your cluster.
  
  7. To navigate back to your deployments, select **Database** from the left-hand menu.
  
img6

### Create a database and collection, and insert our first documents
In this section, we will browse our new **Sandbox** cluster, learn how to create a new database, add a collection, and insert documents.

We will be using the Atlas UI for this section. However, all this can be done with the Atlas CLI and MongoDB Shell.

  1. Click the **Browse Collections** button to access our new **Sandbox** cluster.
  
img7

  2. In the window that appears, select **Add My Own Data.**
  
img8
 
  3. Name our database **Bakery** and our collection **cakes** and hit **Create.**
  
img9
  
  4. We now have our **cakes** collection created inside our new bakery database—woo! But we want to add some data. The Atlas UI makes this really easy. Click the **Insert Document** button in the top right corner.
  
img10

  5. When inserting data in the Atlas UI, you have two options for the view you want for adding data. We want to use the **JSON** view to add some existing cake data easily. Click the **{}** button to switch views.
img11

  6. Delete what is currently in the box, add the following cake document, and then press **Insert.**
```
{
   "name":"Chocolate Cake",
   "shortDescription":"Chocolate cake is a cake flavored with melted chocolate, cocoa powder, or sometimes both.",
   "description":"Chocolate cake is made with chocolate; it can be made with other ingredients, as well. These ingredients include fudge, vanilla creme, and other sweeteners. The history of chocolate cake goes back to 1764, when Dr. James Baker discovered how to make chocolate by grinding cocoa beans between two massive circular millstones.",
   "image":"https://addapinch.com/wp-content/uploads/2020/04/chocolate-cake-DSC_1768.jpg",
   "ingredients":[
      "flour",
      "sugar",
      "cocoa powder"
   ],
   "stock": 25
```

  7. Repeat steps 4 and 5, this time adding the following cake document.
```
{
   "name":"Cheese Cake",
   "shortDescription":"Cheesecake is a sweet dessert consisting of one or more layers. The main, and thickest, layer consists of a mixture of a soft, fresh cheese (typically cottage cheese, cream cheese or ricotta), eggs, and sugar. ",
   "description":"Cheesecake is a sweet dessert consisting of one or more layers. The main, and thickest, layer consists of a mixture of a soft, fresh cheese (typically cottage cheese, cream cheese or ricotta), eggs, and sugar. If there is a bottom layer, it most often consists of a crust or base made from crushed cookies (or digestive biscuits), graham crackers, pastry, or sometimes sponge cake.[1] Cheesecake may be baked or unbaked (and is usually refrigerated).",
   "image":"https://sallysbakingaddiction.com/wp-content/uploads/2018/05/perfect-cheesecake-recipe.jpg",
   "ingredients":[
      "flour",
      "sugar",
      "eggs"
   ],
   "stock": 40
}
```

  8. We want to start storing comments left on each cake and associating them with the cake where the comment was left. Copy the **_id** value from inside the quotes of one of the cake documents you just inserted.
  
img12

  9. To store comments, we want to add a second collection to our **Bakery** database to store the comments that people can leave on each cake. Hover your mouse over **Bakery** in the left panel, and there will be a **+** sign to add a new collection. Click this and add a new collection called **comments.**
  
  img13
  
  10. Add a new document to this new comments collection using the following template, substituting the _id for the one you copied in Step 8, your name, and a comment.
```
{
   "cakeId": "<ID of the Cake Document>",
   "date": "...",
   "name":"<Name>",
   "text":"<Comment>"
}
```

  11. Edit the **comments** document using the edit (pencil) icon in front of the document inserted to change its **Type** from **String** to **ObjectId.** Click **UPDATE** button to save the modification.
  
  img14
  
  img15
  
  Nice! You now have your Atlas database set up with some cake data and even a comment associated with the cake!


## Configure a GraphQL API with Atlas App Services
In this section, we will create our first Atlas App Services application, set some rules for accessing our collections, and then configure a schema for our data, allowing us to enable GraphQL.

### Create an Atlas App Services application

In this section, we will set up our first Atlas App Services application, ready for using GraphQL.

  1. Start by navigating to the **App Services Tab.**

img16

  2. You’ll be prompted to select a starter template. Let’s go with the **Build your own App** option that’s already selected. Click the **Next** button. 
 
img17

  3. Next, you need to configure your application.  
    a. **Data Source:** Since we have created a single cluster, Atlas has already linked it to our application.  
    b. **Application Name:** Let’s give our application a meaningful name, such as **Bakery,** and click **Save.**  
    c. **App Deployment Model:** Change the deployment to **Single Region** and select the region closest to your cluster’s location. Click on the **tick mark** to confirm.
    
img18

  4. Click the Create App Service button to create your first App Services application!

### Configure rules  
We want to add some rules to control our app’s access to our data. We don’t need everything to be able to read and write. So, we will configure those rules in this section.  
  1. At the end of the previous section, after creating your application, it will take you to it in your browser. On the left, under the **Data Access** heading, select **Rules.** 

img19

  2.  We will need to make two rules—one for each of our collections.  
     a. Select the cakes collection, select the readAll preset, and then click Add preset role.  
     b. A popup will appear talking about Save and Deploy. You can just click through this and leave it as it is.  
  3. Select the **comments** collection from the left, and this time, apply the **readAndWriteAll** rule.  
  4. Since we have made changes to the app by adding these rules, we need to deploy those changes. This Review Draft & Deploy step is on by default to protect us from making changes unintentionally.  
     a. Click the **Review Draft & Deploy** button in the blue banner across the top of your screen.  
     b. This will show the rules we have applied, as the system added them to a new rules.json file. Simply scroll down to the bottom of the window and click **Deploy.**
     
### Generate a schema

GraphQL requires a schema to be defined for building up queries, so in this section, we will generate a schema for both our cakes and comments collections.  
  1. Click **Schema** on the left, just below where you clicked **Rules** in Step 1 of the last section.  
  2. Select the **Cakes** collection. App Services will see that you already have data from which it can generate a schema, so click **Define a Schema.**    
  3. Leave the default sample size and click **Generate schema from sampling.**  
  4. A JSON schema will be generated, matching the field names to their data types. At the top of the browser window, click **Save Draft** to save this new schema.  
  5. We now want to generate a schema for our comments collection. Click **Define a Schema**. Then click **or skip and manually define your own schema.** This time, write the schema instead of generating it.

img20

  6. Paste the following JSON schema into the box and click **Save Draft.** You my see a warning message which can be ignored and accepted.  
```
{
  "title": "comment",
  "properties": {
    "_id": {
      "bsonType": "objectId"
    },
    "cakeId": {
      "bsonType": "objectId"
    },
    "date": {
      "bsonType": "date"
    },
    "name": {
      "bsonType": "string"
    },
    "text": {
      "bsonType": "string"
    }
  }
}
```
  7. We now need to define a relationship between our two collections so that the comment document understands cakeId. So, click **Add a relationship** and set it to the following before clicking **Add:**
    - Parent Field: **cakeId - ObjectId**    
    - Linked Database: **Bakery**   
    - Linked Collection: **cakes**  
    - Linked Field: **_id**

  8. At this point, we need to click **Review Draft & Deploy** at the top of the browser window, to deploy both our new schemas for our application.
  9. Click **Deploy** in the modal that pops up.





















  










  

