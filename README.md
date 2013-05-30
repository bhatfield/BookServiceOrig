
## Overview

This sample contains a Node.ACS service that manages book objects and uses
MongoHQ as a backend to manage the data.

Use this sample with the BookClient sample for a demonstration of a client-server
project.

To use this sample, clone this repo, then either import it into Studio or 
run `acs` commands from the cloned directory.

## Import the Sample to Studio

To import this project into Studio:

  1. From the menu bar, select **Import**. The **Import** wizard appears.
  2. Select **General > Existing Folder as New Project**. Click **Next**.
  3. Click **Browse** and navigate to the cloned repo.  Click **Finish**.

Studio creates a new project.

## Configuring BookService

Before running BookService, you need to setup the MongoHQ backend:

  1. Go to http://www.mongohq.com and create an account.
  2. Select to create a free database.
  3. Create a collection called `book`.
  4. In the `controllers/book.js` file, modify the `BASE_URL` variable to point
     to your Mongo URI.  You can find the Mongo URI in the Admin console of your
     database.  It looks similar to 
     `mongodb://foobar:foobar@dharma.mongohq.com:<port_number>/<db_name>`
  
## Running the Service

### Using Studio

In Studio,

  1. Select your project in the **App Explorer** or **Project Explorer** view.
  2. Click on the **Run** button and choose **Local Node.ACS Server**.
  3. Once the service starts, the local port number assigned to the service is
     displayed in the **Console** view.

Use `http://localhost:<port_number>` to access the running service.

### Using the CLI

From the terminal, go to the cloned repo and run the following command:

    acs run
    
Your service can be accessed using http://localhost:8080.
    
## Testing the Service

From a terminal, you can run the following commands:

**Notes:**

  1. You may need to modify your port number in these commands.
  2. `_id` refers to the ID assigned by the Mongo service.

### Create a Book

Command:

    curl -X POST -d "author=<author>" -d "title=<title>" http://localhost:8080/book
    
Example:

    curl -X POST -d "author=Tina Fey" -d "title=Bossypants" http://localhost:8080/book
    
Response:

    {
        "title": "Bossypants",
        "author": "Tina Fey",
        "_id": "51a7ba0793ccb660cd000001"
    }

### Retrieve All Books

Command:

    curl http://localhost:8080/book

Response:

    [
        {
            "title": "Bossypants",
            "author": "Tina Fey",
            "_id": "51a7ba0793ccb660cd000001"
        }
    ]

### Retrieve One Book

Command:

    curl http://localhost:8080/book/_id

Example:

    curl http://localhost:8080/book/51a7ba0793ccb660cd000001
    
Response:

    {
        "title": "Bossypants",
        "author": "Tina Fey",
        "_id": "51a7ba0793ccb660cd000001"
    }

### Modify a Book

Command:

    curl -X PUT -d "author=<author>" -d "title=<title>" http://localhost:8080/book/_id

Example:

    curl -X PUT -d "author=Tina Fey" -d "title=Some Other Book" http://localhost:8080/book/51a7ba0793ccb660cd000001

Reponse:

    {
        "_id": "51a7ba0793ccb660cd000001",
        "title": "Some Other Book",
        "author": "Tina Fey"
    }
     
### Delete a Book

Command:

    curl -X DELETE http://localhost:8080/book/_id

Example:

    curl -X DELETE http://localhost:8080/book/51a7ba0793ccb660cd000001

Response:

    {
        "_id": "51a7ba0793ccb660cd000001",
        "title": "Some Other Book",
        "author": "Tina Fey"
    }


