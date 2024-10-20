# TEDxSDG Search Backend

A semantic search engine that connects TEDx Talks with UN Sustainable Development Goals (SDGs).

## Overview

The **tedxsdg-search-backend** implements semantic search to find relevant TEDx talks (a publicly available dataset) based on SDG-related queries. The system analyzes talk transcripts and descriptions to match them with SDG themes and user queries.

## Technical Implementation

The search engine utilizes several key technologies:

* **TF-IDF** (Term Frequency-Inverse Document Frequency)
  * Converts text data into numerical vectors representing word relevance
  * Enables efficient text comparison and matching

* **Cosine Similarity**
  * Measures similarity between query and document vectors
  * Ranks results based on relevance scores

* **scikit-learn's TfidfVectorizer**
  * Creates sparse TF-IDF matrix from transcripts and descriptions
  * Optimizes memory usage and computation speed

## API Usage

API documentation is available at: [https://tedxsdg-search-backend.vercel.app/api/search/redoc](https://tedxsdg-search-backend.vercel.app/api/search/redoc)

### Example Query

To search for content related to SDG 7 (Affordable and Clean Energy):

```bash
GET https://tedxsdg-search-backend.vercel.app/api/search?query=sdg7
```

### Example Response

```json
{
  "results": [
    {
      "score": 0.540540832015223,
      "document": {
        "slug": "ksenia_petrichenko_what_if_buildings_created_energy_instead_of_consuming_it",
        "description": "Buildings are bad news for the climate -- but they don't have to be…",
        "presenterDisplayName": "Ksenia Petrichenko",
        "transcript": "… Buildings that can consume and produce energy efficiently, interact with a smart grid and respond to its signals, providing flexibility and bringing us closer to our climate targets… ",
        "sdg_tags": [
          "sdg7"
        ]
      }
    }
  ]
}
```

### Response Fields

* `score`: Relevance score based on cosine similarity (0-1)
* `document`: Contains the matched TEDx talk information
  * `slug`: Unique identifier for the talk
  * `description`: Summary of the talk
  * `presenterDisplayName`: Speaker's name
  * `transcript`: Transcript from the talk
  * `sdg_tags`: SDG identifier
