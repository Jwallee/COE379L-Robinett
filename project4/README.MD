The Data Can be downloaded here:
https://huggingface.co/datasets/MongoDB/airbnb_embeddings

You can download the database by making a MongoDB account, and performing the code located at the top of our main project code.

```
import os
from pymongo import MongoClient
import json

# Set up MongoDB Atlas connection URI
uri = os.environ.get('MONGODB_ATLAS_URI')
client = MongoClient(uri)

# Specify your database and collection
db = client['cluster0']  # Replace 'airbnb' with your database name if different
collection = db['airbnb']  # Replace 'airbnb' with your collection name

# Fetch all documents from the collection
data = collection.find({})

# Write data to a JSON file
with open('/Users/grantrobinett/2024/COE379L-Robinett/project4/airbnbData.json', 'w') as file:  # Specify the path to your local JSON file
    file.write('[')
    for index, document in enumerate(data):
        if index != 0:
            file.write(',')
        json.dump(document, file, default=str)  # Convert ObjectId and other BSON types to string
    file.write(']')

print("Data successfully written to JSON file.")
```
