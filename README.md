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






  










  

