# README: GP-FACL Dataset

## 1. Overview

The **GP-FACL Dataset** is a collection of mobile applications identified as fake or potentially fraudulent. It is designed to assist researchers in studying deceptive applications, their characteristics, and user reviews. The dataset includes app metadata, developer details, installation counts, and user reviews to facilitate in-depth analysis of fraudulent app behavior.

This dataset was compiled using a combination of **manual identification** and **automated methods** to detect fake applications. It is useful for **fake app detection**, **fraud analysis**, and **security research** in mobile ecosystems.

## 2. Repository Structure

The repository contains the following files and directories:

- **Final Fake Apps.xlsx**: A spreadsheet containing details of the chosen fake apps, including app metadata and developer information.
- **Dataset/**: A folder containing individual JSON and spreadsheet files, each named after an app’s ID, storing user reviews and additional information.
- **README.md**: This document, providing details on how to use the dataset.

## 3. Dataset Contents

The dataset consists of **two primary components**:

### **A. Fake App Metadata (Final Fake Apps.xlsx)**

This spreadsheet includes detailed information about each identified fake app. The attributes include:

| Column Name            | Description                                                   |
| ---------------------- | ------------------------------------------------------------- |
| **URL**                | The URL of the app in Google Play                             |
| **Appid**              | Unique identifier for the app (package name).                 |
| **App Title**          | The name of the application.                                  |
| **Summary**            | The summary of the app shown in Google Play                   |
| **Description**        | The summary of the app provided by the publisher              |
| **Genre**              | The category of the app (e.g., Finance, Tools, Social, etc.). |
| **Release Time**       | The initial release date of the application.                  |
| **Update Time**        | The last recorded update date of the app.                     |
| **Score**              | The average user rating (out of 5).                           |
| **Real Installs**      | Estimated number of actual installations.                     |
| **Total Reviews**      | The total number of user reviews.                             |
| **Dev Website**        | URL of the developer's website (if available).                |
| **Dev Email**          | Email contact of the developer.                               |
| **Dev Address**        | Physical address of the developer (if available).             |
| **Dev Website Flag**   | Whether or not the app has triggered the website flag         |
| **Dev Address Flag**   | Whether or not the app has triggered the address flag         |
| **Update Time Flag**   | Whether or not the app has triggered the update time flag     |
| **Real installs Flag** | Whether or not the app has triggered the installs flag        |
| **Fake**               | Whether or not the app has been confirmed as fake             |
| **Reason**             | Our reason for labeling the app as fake                       |

### **B. User Reviews (Dataset Folder)**

Each app's reviews are stored in **JSON and spreadsheet files** inside the `Dataset/` folder. The files are named after their respective App IDs. Each JSON file contains structured user reviews with the following attributes:

```json
{
  "appVersion": "1.0.0",
  "at": "2023-08-26 21:42:18",
  "content": "I. verify your nubber",
  "repliedAt": null,
  "replyContent": null,
  "reviewCreatedVersion": "1.0.0",
  "reviewId": "bb0668e8-e1b1-4b6f-ab7f-5dc7cd49ac8f",
  "score": 3,
  "thumbsUpCount": 1,
  "userImage": "https://play-lh.googleusercontent.com/a/ACg8ocJ9smsdyD5U192jQez61k0-7v-RImEh-fZusE1ng66j=mo",
  "userName": "Mojahid Ansari"
}
```

Each spreadsheet file in the `Dataset/` folder contains the same review data in tabular format for easier analysis.

## 4. Usage Instructions

### **A. Loading the Dataset in Python**

```python
import pandas as pd

# Load the fake apps metadata
metadata_path = "Final Fake Apps.xlsx"
df_metadata = pd.read_excel(metadata_path)

# Display first few rows
df_metadata.head()
```

### **B. Accessing User Reviews**

```python
import json

# Load a sample review file
review_file = "Dataset/and.iverify.app.json"
with open(review_file, "r") as file:
    reviews = json.load(file)

# Display the first review
print(reviews[0])
```

## 5. Example Analyses

### **A. Fake App Distribution by Category**

```python
import matplotlib.pyplot as plt

# Plot category distribution
df_metadata['Genre'].value_counts().plot(kind='bar', title='Fake Apps by Category')
plt.xlabel("Category")
plt.ylabel("Number of Fake Apps")
plt.show()
```

### **B. Identifying Removed Apps**

Apps removed from Google Play can be filtered as follows:

```python
removed_apps = df_metadata[df_metadata["Reason"].str.contains("removed", case=False, na=False)]
print(removed_apps[["App Title", "Reason"]])
```
