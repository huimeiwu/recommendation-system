# Two-Tier Recommendation Recommendation System for Cold-Start Users

This project builds a **two-tier recommendation system** for a dessert brand expanding into the U.S. market. Since many customers are unfamiliar with the dessert style and have no prior interaction history, we focused on helping new users discover items they might enjoy through a structured ingredient-based approach.

Note: For privacy reasons, the raw POS sales data used to generate ingredient preference signals is not uploaded to this repo. However, all preprocessing and modeling scripts are included and can be adapted to other data sources.

## Project Highlights

### Two-Tier Recommendation Architecture

We designed a **layered recommendation pipeline** to improve flexibility, interpretability, and cold-start performance:

#### **Ingredient-Level Preference Modeling (Primary Contribution)**

My primary contribution focused on the ingredient-level preference modeling layer, including data simulation, representation learning, and evaluation under sparse and cold-start conditions.

We modeled user preferences at the ingredient level (e.g., boba, taro, grass jelly) rather than full menu items to capture shared preference signals across products with overlapping components.

- Designed a synthetic user–ingredient interaction matrix to approximate realistic preference signals under limited explicit feedback, using POS frequency signals and MovieLens-inspired sampling.
- Trained an ALS-based collaborative filtering model in PySpark to learn stable ingredient embeddings under high sparsity.
- Stored learned user and ingredient embeddings in BigQuery to support efficient downstream retrieval and analysis.
- Evaluated model quality using precision@5 (0.63) and ingredient coverage (90%), prioritizing discovery and diversity for cold-start users.

#### **Product-Level Mapping & Recommendation (System Context)**

The second layer maps learned ingredient preferences to actual menu items, providing a lightweight bridge from ingredient-level signals to product-level recommendations.

- Used ingredient-overlap scoring to rank menu items based on preferred ingredients.
- Implemented TF-IDF similarity on product descriptions as a fallback for cold-start scenarios (e.g., new users or sparse ingredient signals).
- Integrated with downstream systems via APIs to support UI rendering and experimentation workflows.

This modular design enables the system to surface new or unfamiliar products by translating latent ingredient preferences into interpretable product-level recommendations.

## Technologies Used

- PySpark & ALS (Spark MLlib)
- Python (Pandas, NumPy, scikit-learn)
- TF-IDF (text similarity)
- BigQuery (embedding storage)
- Jupyter Notebooks (experimentation)

## Collaboration Context

This project was developed during an internship at JoblogicX in collaboration with ML engineers, data engineers, and product designers. I focused on the ingredient-level modeling layer and worked closely with teammates to ensure alignment with downstream product-level ranking and experimentation workflows.




