# Full-Stack Development & Deployment Architecture on Google Cloud

This document outlines the complete lifecycle of the application, from local development to production deployment and operations on Google Cloud.

### **1. Local Development: A High-Velocity, Hot-Reload Setup**

The goal is a seamless "inner loop" where changes are reflected instantly.

*   **Frontend (Vite):** Your current Vite setup already provides best-in-class hot-reloading for the React frontend via the `npm run dev` command. No changes are needed here.
*   **Backend (Node.js/Python):**
    *   **Node.js:** Use `nodemon` to watch for file changes and automatically restart the server.
    *   **Python (FastAPI):** The development server has this built-in. Run it with `uvicorn main:app --reload`.
*   **Unified Local Environment (Recommended):**
    *   **Tooling:** Use a tool like `concurrently` to run both frontend and backend dev servers with a single command.
    *   **Containerization (`docker-compose`):** This is the **best practice**. Create a `docker-compose.yml` file to define and run your entire local stack: the frontend container, the backend container, and a local Postgres database container.
        *   **Benefit:** A single command (`docker-compose up`) starts everything. Every developer gets the exact same setup, eliminating "it works on my machine" issues.

### **2. Deployment: Serverless & Scalable with Cloud Run**

Cloud Run is the ideal target for containerized applications, offering auto-scaling (even to zero) and a simple developer experience.

*   **Strategy:** Deploy the frontend and backend as two separate, independent Cloud Run services.
    *   **Frontend Service:** A `Dockerfile` will build the React app and use a lightweight web server like **Nginx** to serve the static files.
    *   **Backend Service:** A `Dockerfile` will package your Node.js or Python application.
*   **Communication:** The frontend service will be configured with the public URL of the backend service to make API calls.
*   **Security:**
    *   The frontend service should be public.
    *   The backend service should be configured to only accept requests from the frontend service and authenticated users.

### **3. API Integration: Securely Using Gemini on Vertex AI**

Using Vertex AI is the enterprise-grade way to use Gemini models.

*   **Authentication:** **Do not use API keys in production.** Instead, use **Workload Identity**.
    1.  Create a dedicated **IAM Service Account** for your backend service (e.g., `my-app-backend-sa`).
    2.  Grant this service account the `Vertex AI User` role.
    3.  Configure your backend's Cloud Run service to use this service account.
*   **Benefit:** Your application code automatically and securely authenticates to the Vertex AI API using Google Cloud's infrastructure. No keys to manage or leak.

### **4. Database & Storage: Choosing the Right Tool for the Job**

Google Cloud offers a suite of databases. Using the right one is critical for performance and cost.

| Database / Storage | Data Model             | Use Case                                                                                             | When to Choose It                                                                                             |
| ------------------ | ---------------------- | ---------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| **Firestore**      | NoSQL (Documents)      | User profiles, real-time chat, activity feeds, semi-structured data.                                 | You need rapid development, automatic scaling, and easy synchronization with web/mobile clients.              |
| **Cloud SQL**      | Relational (Postgres)  | **Your default choice.** E-commerce orders, financial data, user credentials, any structured data.     | You need ACID compliance, complex queries, joins, and the reliability of a traditional relational database.    |
| **Cloud Spanner**  | Relational (Global)    | Global financial ledgers, massive-scale inventory systems, multi-region applications.                | You need the consistency of SQL but at a global scale that exceeds Cloud SQL's limits. This is for huge apps. |
| **Bigtable**       | NoSQL (Wide-column)    | IoT sensor data, ad-tech analytics, monitoring metrics.                                              | You have massive (terabytes+) datasets with very high write and read throughput needs.                        |
| **BigQuery**       | Analytical Warehouse   | Business intelligence dashboards, log analysis, feeding data to ML models.                           | You need to run complex analytical queries on huge datasets. **It is not a transactional database.**          |
| **Cloud Storage**  | Object Storage         | User-uploaded images/videos, static assets, backups, data lake storage.                              | For storing unstructured files. Your application will store the *URL* to the object in a database like Cloud SQL. |

### **5. CI/CD: Automated Builds & Deployments**

Automate your path from code to production using a GitOps workflow.

1.  **Source:** Connect your GitHub repository to **Cloud Build**.
2.  **Build (`cloudbuild.yaml`):** In your repository, create a `cloudbuild.yaml` file. When code is pushed to the `main` branch, it will trigger Cloud Build to:
    *   Install dependencies (`npm install`, `pip install`).
    *   Run all tests.
    *   Build the frontend and backend Docker images.
    *   Push the versioned images to **Artifact Registry**.
3.  **Deploy (`clouddeploy.yaml`):** Cloud Build will then trigger a **Cloud Deploy** pipeline.
    *   **Delivery Pipeline:** Define your promotion path (e.g., `dev` -> `staging` -> `prod`).
    *   **Targets:** Each target is a different Cloud Run environment.
    *   **Benefit:** This gives you safe, auditable, one-click promotions, and instant rollbacks.

### **6. Other Essential Cloud Services: The Supporting Cast**

These services are non-negotiable for a production-grade application.

*   **Secret Manager:** For all secrets: database passwords, third-party API keys, etc. Your Cloud Run services will be granted secure access at runtime.
*   **IAM (Identity and Access Management):** Enforce the **Principle of Least Privilege**. Services and developers should only have the exact permissions they need.
*   **Cloud Logging & Monitoring:** Your eyes and ears. All Cloud Run services automatically stream logs here. Set up dashboards and alerts to monitor application health and performance.
*   **VPC & Serverless VPC Access Connector:** This is **critical** for connecting your Cloud Run service to your Cloud SQL database securely and with low latency over a private network.
*   **Cloud Armor:** A Web Application Firewall (WAF) to protect your public-facing frontend from common web attacks and DDoS attempts.
