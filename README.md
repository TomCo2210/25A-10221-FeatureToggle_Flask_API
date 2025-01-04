# 25A-10221-FeatureToggl_Flask_API

- Flask
- Flasgger (Flask Swagger)
- MongoDB Connection
- HTTP 
- Vercel Deployment

# Feature Toggle API

This API provides functionality for managing feature toggles in a MongoDB-backed system. Feature toggles allow selective activation or deactivation of features for specific packages, enabling flexible feature rollout strategies.

---

## Endpoints

### 1. Create a New Feature Toggle
**POST /feature-toggle**

**Description:**
Creates a new feature toggle for a specific package.

**Request Body:**
```json
{
  "package_name": "string",
  "name": "string",
  "description": "string",
  "beginning_date": "YYYY-MM-DD HH:MM:SS",
  "expiration_date": "YYYY-MM-DD HH:MM:SS"
}
```

**Responses:**
- **201:** Feature toggle created successfully.
- **400:** Invalid request or date format.
- **500:** Database connection error.

---

### 2. Get All Feature Toggles for a Package
**GET /feature-toggles/<package_name>**

**Description:**
Retrieves all feature toggles for the specified package.

**Path Parameters:**
- `package_name` (string): Name of the package.

**Responses:**
- **200:** List of feature toggles.
- **404:** Package not found.
- **500:** Database connection error.

---

### 3. Get a Feature Toggle by ID
**GET /feature-toggle/<package_name>/<feature_id>**

**Description:**
Retrieves details of a specific feature toggle by its ID.

**Path Parameters:**
- `package_name` (string): Name of the package.
- `feature_id` (string): ID of the feature toggle.

**Responses:**
- **200:** Feature toggle details.
- **404:** Feature toggle not found.
- **500:** Database connection error.

---

### 4. Get Active Feature Toggles
**GET /feature-toggles/<package_name>/active**

**Description:**
Retrieves all active feature toggles for a specified package. Active toggles are those whose current date falls between their `beginning_date` and `expiration_date`.

**Path Parameters:**
- `package_name` (string): Name of the package.

**Responses:**
- **200:** List of active feature toggles.
- **404:** Package not found.
- **500:** Database connection error.

---

### 5. Get Feature Toggles by Date
**GET /feature-toggles/<package_name>/by-date**

**Description:**
Retrieves feature toggles active on a specified date.

**Path Parameters:**
- `package_name` (string): Name of the package.

**Query Parameters:**
- `date` (string, required): Date in the format `YYYY-MM-DD`.

**Responses:**
- **200:** List of feature toggles active on the specified date.
- **400:** Invalid date format.
- **404:** Package not found.
- **500:** Database connection error.

---

### 6. Update Feature Toggle Dates
**PUT /feature-toggle/<package_name>/<feature_id>/update-dates**

**Description:**
Updates the `beginning_date` and/or `expiration_date` of a specific feature toggle.

**Path Parameters:**
- `package_name` (string): Name of the package.
- `feature_id` (string): ID of the feature toggle.

**Request Body:**
```json
{
  "beginning_date": "YYYY-MM-DD HH:MM:SS",
  "expiration_date": "YYYY-MM-DD HH:MM:SS"
}
```

**Responses:**
- **200:** Dates updated successfully.
- **400:** Invalid date format or logic.
- **404:** Feature toggle not found.
- **500:** Database connection error.

---

### 7. Delete All Feature Toggles for a Package
**DELETE /feature-toggles/<package_name>**

**Description:**
Deletes all feature toggles for a specific package.

**Path Parameters:**
- `package_name` (string): Name of the package.

**Responses:**
- **200:** All feature toggles deleted.
- **404:** Package not found.
- **500:** Database connection error.

---

### 8. Delete All Feature Toggles
**DELETE /feature-toggles**

**Description:**
Deletes all feature toggles across all packages.

**Responses:**
- **200:** All feature toggles deleted.
- **500:** Database connection error.

---

## Notes
- All dates must be in the format `YYYY-MM-DD HH:MM:SS`.
- MongoDB is used as the database backend. Ensure the `MongoConnectionHolder` is correctly configured.
- Error handling is implemented for invalid input, database connection failures, and other edge cases.

## Setup Instructions
1. Install dependencies:
   ```bash
   pip install -r ./requirements.txt
   ```
2. Ensure MongoDB is running and accessible.
3. Start the Flask application.
    ```bash
    python app.py
    ```

---

## License
This API is provided under the MIT License. Feel free to modify and use it as needed.
