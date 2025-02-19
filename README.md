# Youtube-Manager-Mongodb
## Project Overview
The goal of this project is to manage YouTube videos, allowing users to add, update, delete, and list videos. We will utilize MongoDB as our database to store video information, and Python will serve as our programming language.

## Setting Up MongoDB Atlas
Before we start coding, we need to set up our MongoDB database. We will use MongoDB Atlas, a cloud-based database service. Here are the steps to get started:

Create an Account: Go to the MongoDB Atlas website and create a free account.
Create a Project: Once logged in, create a new project in Atlas.
Network Access: Allow access to your database by adding your IP address (0.0.0.0/0) to the network access list.
Database User: Create a new database user with read and write access.
Connection String: Obtain the connection string for your database, which will be used in our Python code.
## Installing Required Packages
To interact with MongoDB using Python, we need to install the pymongo package. You can install it using pip:

pip install pymongo
## Coding the Application
Now that we have our database set up and the necessary packages installed, let's start coding our YouTube manager application.

### Basic Structure
We will create a Python script that will handle the main functionalities of our application. Here’s a basic outline of our script:

Import Libraries: Import the necessary libraries, including pymongo.
Connect to MongoDB: Use the connection string to connect to our MongoDB database.
Define Functions: Create functions for adding, updating, deleting, and listing videos.
User Interface: Implement a simple command-line interface for user interaction.
### Connecting to MongoDB
Here’s how to connect to MongoDB using pymongo:

from pymongo import MongoClient


client = MongoClient('your_connection_string')
db = client['youtube_manager']
### Defining Functions
Next, we will define the functions for our application:

Adding a Video
def add_video(name, time):
    video_collection = db['videos']
    video_collection.insert_one({'name': name, 'time': time})
Listing Videos
def list_videos():
    video_collection = db['videos']
    for video in video_collection.find():
        print(f"ID: {video['_id']}, Name: {video['name']}, Time: {video['time']}")
Updating a Video
def update_video(video_id, new_name, new_time):
    video_collection = db['videos']
    video_collection.update_one({'_id': video_id}, {'$set': {'name': new_name, 'time': new_time}})
Deleting a Video
def delete_video(video_id):
    video_collection = db['videos']
    video_collection.delete_one({'_id': video_id})
### User Interface
Finally, we will implement a simple command-line interface to interact with our application:

while True:
    print("1. Add Video")
    print("2. List Videos")
    print("3. Update Video")
    print("4. Delete Video")
    print("5. Exit")
    choice = input("Enter your choice: ")

    if choice == '1':
        name = input("Enter video name: ")
        time = input("Enter video time: ")
        add_video(name, time)
    elif choice == '2':
        list_videos()
    elif choice == '3':
        video_id = input("Enter video ID to update: ")
        new_name = input("Enter new video name: ")
        new_time = input("Enter new video time: ")
        update_video(video_id, new_name, new_time)
    elif choice == '4':
        video_id = input("Enter video ID to delete: ")
        delete_video(video_id)
    elif choice == '5':
        break
    else:
        print("Invalid choice. Please try again.")
## Debugging and Troubleshooting
During the development process, you may encounter various issues, especially with database connections and data handling. Here are some common troubleshooting tips:

Connection Issues: Ensure your connection string is correct and that your IP address is whitelisted in MongoDB Atlas.
Data Types: Be mindful of data types when passing values to MongoDB. For example, ObjectIDs must be handled correctly.
Error Handling: Implement try-except blocks to catch and handle exceptions gracefully.
## Conclusion
In this blog post, we successfully built a YouTube manager application using Python and MongoDB. We covered the setup process, coding practices, and troubleshooting tips. This project not only enhances your Python skills but also provides a practical understanding of working with databases.
