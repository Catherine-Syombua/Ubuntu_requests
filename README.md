# Ubuntu_requests
This is a program that ties technical practice to ubuntu
[Ubuntu_requests.py](https://github.com/user-attachments/files/23051007/Ubuntu_requests.py)# ubuntu_image_fetcher.py

import os
import requests
from urllib.parse import urlparse
import uuid  # for generating a unique filename if none exists

def fetch_image():
    print("🌍 The Wisdom of Ubuntu: 'I am because we are'")
    print("Let's fetch and share beauty from the global community.\n")

    # Ask the user for an image URL
    url = input("Please enter the URL of the image you want to fetch: ").strip()

    # Create directory to store fetched images
    save_dir = "Fetched_Images"
    os.makedirs(save_dir, exist_ok=True)  # Respectfully create directory if it doesn't exist

    try:
        # Attempt to fetch the image
        print("\n🔗 Connecting to the community...")
        response = requests.get(url, timeout=10)
        response.raise_for_status()  # Raise an error for bad HTTP status codes

        # Extract filename from URL
        parsed_url = urlparse(url)
        filename = os.path.basename(parsed_url.path)

        # If no filename found, generate one using uuid
        if not filename:
            filename = f"image_{uuid.uuid4().hex}.jpg"

        # Full path for saving
        filepath = os.path.join(save_dir, filename)

        # Save image in binary mode
        with open(filepath, "wb") as file:
            file.write(response.content)

        print(f"✅ Image successfully fetched and saved as: {filepath}")
        print("🤝 Ubuntu spirit upheld — sharing and organizing complete.")

    except requests.exceptions.MissingSchema:
        print("❌ Invalid URL. Please ensure it starts with http:// or https://.")
    except requests.exceptions.ConnectionError:
        print("⚠️ Could not connect. Please check your internet connection or the URL.")
    except requests.exceptions.Timeout:
        print("⌛ Connection timed out. The server might be busy or unreachable.")
    except requests.exceptions.HTTPError as e:
        print(f"❌ HTTP Error: {e}")
    except Exception as e:
        print(f"⚠️ An unexpected error occurred: {e}")

# Run the program
if __name__ == "__main__":
    fetch_image()

