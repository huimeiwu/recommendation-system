# Two-Tier Recommendation Recommendation System for Cold-Start Users

This project builds a **two-tier recommendation system** for a dessert brand expanding into the U.S. market. Since many customers are unfamiliar with the dessert style and have no prior interaction history, we focused on helping new users discover items they might enjoy through a structured ingredient-based approach.

Note: For privacy reasons, the raw POS sales data used to generate ingredient preference signals is not uploaded to this repo. However, all preprocessing and modeling scripts are included and can be adapted to other data sources.

## Project Highlights

### Two-Tier Recommendation Architecture

We designed a **layered recommendation pipeline** to improve flexibility, interpretability, and cold-start performance:

#### **Ingredient-Level Preference Modeling**

My primary contribution focused on the ingredient-level preference modeling layer, including data simulation, representation learning, and evaluation under sparse and cold-start conditions.

Instead of starting with full menu items, we first model user preferences at the ingredient level (e.g., boba, taro, grass jelly). This enables the system to capture shared signals across products that use similar components.  

- Designed a synthetic user–ingredient interaction matrix to approximate realistic preference signals under limited explicit feedback, using POS frequencies and       MovieLens-inspired sampling.
- Trained an ALS-based collaborative filtering model in PySpark to learn stable ingredient embeddings under high sparsity.
- Stored learned user and ingredient embeddings in BigQuery to support efficient downstream retrieval and analysis.
- Evaluated model quality using precision@5 (0.63) and ingredient coverage (90%), prioritizing discovery and diversity for cold-start users.

#### **Product-Level Mapping & Recommendation**

The second layer connects ingredient preferences to actual menu items. This layer provides a lightweight mapping from ingredient preferences to menu items and serves as contextual background for the overall system.

- Used **ingredient-overlap scoring** to rank menu items based on preferred ingredients.
- Implemented **TF-IDF similarity** on product descriptions to build a fallback for cold-start cases (e.g., new users or sparse ingredients).
- Exposed APIs to downstream systems for UI rendering and experimentation teams.

This modular design helps the system recommend new or unfamiliar products by leveraging latent preferences over ingredients, which are more transferable and easier to interpret.

## Technologies Used

- PySpark & ALS (Spark MLlib)
- Python (Pandas, NumPy, scikit-learn)
- TF-IDF (text similarity)
- BigQuery (embedding storage)
- Jupyter Notebooks (experimentation)

## Collaboration Context

This was developed during an internship at **JoblogicX**, working with a cross-functional team of ML engineers, data engineers, and product designers. I focused on the ingredient-level layer and ensured seamless integration into downstream systems.




