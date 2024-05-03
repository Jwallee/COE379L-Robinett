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

Downloading Images can be done here:
```
import os
import json
import requests

def ensure_dir(directory):
    if not os.path.exists(directory):
        os.makedirs(directory)

def download_image(image_url, path_to_save):
    try:
        response = requests.get(image_url, stream=True, timeout=10)  # 10-second timeout
        if response.status_code == 200:
            with open(path_to_save, 'wb') as out_file:
                out_file.write(response.content)
            return True
    except requests.RequestException as e:
        print(f"Error downloading {image_url}: {e}")
    return False

def process_images(json_path, output_dir, log_file):
    with open(json_path, 'r') as file:
        listings = json.load(file)

    unsuccessful_ids = []

    for listing in listings:
        listing_id = listing['_id']
        images = listing.get('images', {})
        directory_path = os.path.join(output_dir, str(listing_id))
        ensure_dir(directory_path)

        success = False
        for key, url in images.items():
            if url:  # Check if the URL is not empty
                file_name = url.split('/')[-1].split('?')[0]  # Simplistic way to get file name from URL
                full_path = os.path.join(directory_path, file_name)
                if download_image(url, full_path):
                    print(f"Successfully downloaded {full_path}")
                    success = True
                else:
                    print(f"Failed to download from {url}")

        if not success:
            unsuccessful_ids.append(listing_id)

    # Log unsuccessful IDs
    if unsuccessful_ids:
        with open(log_file, 'w') as f:
            for id in unsuccessful_ids:
                f.write(f"{id}\n")
        print(f"Logged unsuccessful download IDs to {log_file}")

# Example usage
process_images('/Users/grantrobinett/2024/COE379L-Robinett/project4/airbnbData.json', 'imagesData', 'unsuccessful_downloads.log')
```
