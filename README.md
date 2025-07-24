# 🏭 Smart Factory Agentic AI Demo

This project demonstrates a lightweight, browser-based Agentic AI application designed for a simulated smart factory environment. It showcases how an AI agent can intelligently combine information from diverse data sources and trigger "ML models" to provide comprehensive, context-rich responses to complex natural language queries.

## ✨ Project Overview

The core idea is an intelligent **"Factory Advisor"** agent. This agent doesn't just answer questions from static documents; it dynamically navigates a simulated Smart Factory ecosystem. It understands your query, decides which information sources are relevant (documents, databases, real-time sensor data), and even determines when to invoke specialized ML models (like defect detection or predictive maintenance) to gather additional, dynamic context before synthesizing a comprehensive and actionable response.

This demo aims to illustrate the immense potential of Agentic RAG to empower factory workers and personnel across all disciplines by providing holistic and diverse context for their queries.

## 🧠 Logic Behind the Code (Agentic Workflow)

The application implements the core concepts of an agentic workflow, similar to what frameworks like LangChain enable:

1.  **User Query:** The user inputs a natural language query (e.g., "MachineA is showing an unexpected drop in output quality today, what could be wrong, and what's the recommended fix?").
2.  **LLM as Agent's Brain:** A Large Language Model (LLM) (simulated via Gemini API) acts as the central agent. It interprets the query, understands the user's intent, and decides on the best course of action.
3.  **Tool Selection & Execution:** The agent has access to a set of predefined "tools" (JavaScript functions mimicking external systems or ML models). Based on its reasoning, it selects and calls the most appropriate tool(s).
    * The LLM generates a JSON object specifying the `tool` to call and its `tool_input`.
    * The JavaScript code executes the corresponding simulated tool function.
4.  **Iterative Reasoning:** The output from a tool is fed back to the LLM. The agent can then decide to call another tool to gather more context, or if it has sufficient information, formulate a final comprehensive answer.
5.  **Retrieval Augmented Generation (RAG):** For queries requiring document-based knowledge, a `retrieve_document_context` tool is used. This simulates fetching relevant information from a knowledge base (documents stored in Firestore).
6.  **Holistic Response Generation:** Once all necessary information is gathered, the LLM synthesizes a structured, easy-to-read response, combining insights from all utilized data sources.

## 🛠️ Essential Components & Simulated Data Sources

This demo conceptually integrates various components and data sources found in a smart factory:

* **The "Brain": Large Language Model (LLM)**
    * **Role:** Interprets user queries, orchestrates the workflow, and synthesizes responses.
    * **Implementation:** Powered by the Gemini API (`gemini-2.0-flash`).
* **The "Knowledge Base": Retrieval Augmented Generation (RAG)**
    * **Role:** Provides contextual information from unstructured documents.
    * **Implementation:** Simulated documents (SOPs, Technical Specifications) stored in **Firestore Database**. The `retrieve_document_context` tool performs a basic keyword search on these documents.
* **The "Tools": Simulated Factory Systems & ML Models**
    * **`get_sensor_data`:** Mimics a historian/time-series dataset, providing real-time sensor readings (e.g., vibration, temperature, pressure).
    * **`run_predictive_maintenance_model`:** Simulates an ML model, forecasting potential machine failures (e.g., Tool Wear Failure).
    * **`get_mes_production_status`:** Represents a Manufacturing Execution System (MES), providing production rates, quality checks, and work orders.
    * **`check_erp_inventory`:** Simulates an Enterprise Resource Planning (ERP) system, checking inventory levels for spare parts.
    * **`get_camera_anomaly_report`:** Mimics a vision system, providing reports on detected defects from production line cameras.

## 🎯 How a Specific Data Source is Utilized (Example)

Consider the query: **"MachineA is showing an unexpected drop in output quality today, what could be wrong, and what's the recommended fix?"**

The agent's workflow would typically involve:

1.  **Initial RAG:** Retrieve relevant SOPs and technical specifications for "MachineA" and "quality issues."
2.  **Sensor Data:** Use `get_sensor_data` to fetch current vibration, temperature, and pressure readings for "MachineA."
3.  **Predictive Maintenance:** Call `run_predictive_maintenance_model` with the sensor data to get a diagnosis (e.g., "high probability of Tool Wear Failure").
4.  **MES Data:** Use `get_mes_production_status` to confirm the actual production rate and recent quality check results for "MachineA."
5.  **Synthesis:** Combine all this information (SOPs, sensor data, ML prediction, MES data) to provide a structured answer, including diagnosis, impact, and recommended troubleshooting steps from the SOP.

## 🚀 Real-World Technology Stack Considerations

For a production-grade implementation of such an Agentic RAG system in a smart factory, the technology stack would typically look like this:

* **Agent Frameworks:** LangChain (Python/JS), LlamaIndex (Python), Marvin (Python), AutoGen (Python) for orchestrating complex agent behaviors.
* **Large Language Models (LLMs):** Enterprise-grade models like Google's Gemini, OpenAI's GPT series, or fine-tuned open-source models (Llama, Mixtral) hosted on secure infrastructure.
* **Vector Databases:** Scalable solutions like MongoDB, PostgreSQL, Chroma, Weaviate, Pinecone, Qdrant, or Elasticsearch (with vector search) for efficient semantic search over documents.
* **Data Integration & Unified Namespace (UNS):**
    * **MQTT Brokers:** HiveMQ, Mosquitto, EMQX for real-time data streaming from IoT devices and PLCs.
    * **OPC UA:** For standardized communication with industrial control systems.
    * **Kafka:** For high-throughput data pipelines and event streaming.
    * **HighByte:** For Industrial DatOps.
    * **Data Historians:** PI System, OSIsoft PI, AspenTech InfoPlus.21 for long-term storage of time-series data.
* **Manufacturing Execution Systems (MES) & Enterprise Resource Planning (ERP):** Integration via their native APIs or custom connectors (e.g., SAP, Oracle, Siemens Opcenter).
* **ML Model Serving:** FastAPI (for custom Python APIs), TensorFlow Serving, TorchServe, NVIDIA Triton Inference Server for exposing trained ML models as callable services.
* **Cloud Platforms:** AWS, Azure, Google Cloud for scalable hosting of LLMs, vector databases, agent orchestrators, and ML model serving infrastructure. For on-premise deployments, Kubernetes is a common choice. 

## 📈 Benefits for Manufacturers

Implementing an Agentic RAG system like this can yield significant benefits:

* **Enhanced Decision-Making:** Provides faster, more accurate, and data-driven insights to all levels of personnel.
* **Proactive Problem Solving:** Identifies potential issues (e.g., machine failures, quality deviations) before they escalate, minimizing downtime and waste.
* **Increased Efficiency & Productivity:** Automates information retrieval, streamlines troubleshooting, and reduces the time spent searching for answers across disparate systems.
* **Empowered Workforce:** Equips factory workers, engineers, and managers with immediate, relevant, and comprehensive information, fostering a more autonomous and capable team.
* **Improved Quality & Consistency:** By leveraging real-time data and ML insights, it helps maintain product quality and process consistency.
* **Reduced Operational Costs:** Minimizes manual intervention, optimizes resource utilization, and prevents costly failures.

This project offers a glimpse into the future of intelligent manufacturing, where AI acts as a true partner in optimizing factory operations.

---

## 🚀 How to Run the Demo

To run this demo on your local machine:

1.  **Save the Code:** Copy the entire HTML code (from `<!DOCTYPE html>` to `</html>`) into a file named `index.html` (or any `.html` file) using a plain text editor.
2.  **Configure Firebase (Crucial for Data Persistence):**
    * Go to [Firebase Console](https://console.firebase.google.com/).
    * Create a new project.
    * Add a "Web app" to your project. Firebase will provide a `firebaseConfig` JavaScript object. **Copy this object.**
    * In your Firebase project, navigate to **"Build" > "Firestore Database"** and **"Rules"** tab. Replace the default rules with the following to allow authenticated users (including anonymous) to read/write public data:
        ```firestore
        rules_version = '2';
        service cloud.firestore {
          match /databases/{database}/documents {
            match /artifacts/{appId}/public/data/{collectionId}/{document=**} {
              allow read, write: if request.auth != null;
            }
          }
        }
        ```
        Click **"Publish Rules"**.
    * Go to **"Build" > "Authentication"** and enable the **"Anonymous"** sign-in method under the "Sign-in method" tab.
    * In your `index.html` file, find the `firebaseConfig` placeholder and **replace it with the `firebaseConfig` object you copied from your Firebase Console.**
        ```javascript
        const firebaseConfig = {
            // PASTE YOUR ACTUAL FIREBASE CONFIG OBJECT HERE
            apiKey: "YOUR_API_KEY",
            authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
            projectId: "YOUR_PROJECT_ID",
            storageBucket: "YOUR_PROJECT_ID.appspot.com",
            messagingSenderId: "YOUR_SENDER_ID",
            appId: "YOUR_APP_ID"
        };
        ```
3.  **Insert Gemini API Key (Crucial for LLM Interaction):**
    * Obtain a Gemini API key from [Google AI Studio](https://aistudio.google.com/app/apikey).
    * In your `index.html` file, find the `const apiKey = "";` line and **insert your Gemini API key** between the quotes:
        ```javascript
        const apiKey = "YOUR_GEMINI_API_KEY_HERE";
        ```
4.  **Open in Browser:** Double-click your `index.html` file. It will open in your default web browser.

### 📋 Example Queries to Try:

* "MachineA is showing an unexpected drop in output quality today, what could be wrong, and what's the recommended fix?"
* "Tell me about the normal operating parameters for MachineA."
* "Do we have spare Tool\_A\_Spare units in inventory?"
* "Are there any recent anomaly reports from ProductionLine\_Camera\_1?"
* "What are the common defects classified in production line quality control?"

## 📦 Dependencies

This project is a pure client-side HTML/JavaScript application. All external dependencies are loaded via Content Delivery Networks (CDNs), so you only need an internet connection:

* **Tailwind CSS:** For styling and responsive design.
    * `https://cdn.tailwindcss.com`
* **Firebase SDK (v11.6.1):** For interacting with Firestore (to store and retrieve RAG documents) and Firebase Authentication.
    * `https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js`
    * `https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js`
    * `https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js`
* **Gemini API:** For the Large Language Model interactions. This is called directly via `fetch` requests.

---
**Note:** This demo uses simulated data for factory systems and ML models for simplicity. A real-world implementation would involve integrating with actual factory APIs, databases, and deployed ML services.
