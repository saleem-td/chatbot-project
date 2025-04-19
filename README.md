Stage 1 - Basic Chatbot

In this stage, we build a basic chatbot using Streamlit and the OpenAI API. The chatbot provides a simple user interface where users can interact and receive AI-generated responses.
At this stage, the chatbot runs entirely on the frontend, meaning Streamlit directly communicates with the OpenAI API. This setup serves as the foundation for later stages, where we will introduce a backend and enhance functionality.

<img src="/assets/St-1.png" width="650"/>

---

Stage 2 - Basic Chatbot with FastAPI

In this stage, we enhance our basic chatbot by introducing FastAPI as a backend service. Instead of making direct calls to the OpenAI API from the frontend, we now handle these requests through the FastAPI backend.

With this setup, when a user interacts with the Streamlit frontend, their request is sent to the FastAPI backend, which then calls the OpenAI API and returns the response.

By separating responsibilities, the frontend focuses on user interaction and session management, while the backend handles business logic and API calls. This modular approach ensures that as long as the backend is running, the frontend can be replaced or updated with another technology without affecting core functionality.

<img src="/assets/St-2.png" width="650"/>

---

Stage 3 - Chatbot with Chat History

In this stage, we enhance our basic chatbot, built with Streamlit and FastAPI, by adding chat history storage. Now, conversations are saved locally, and session details are logged in a PostgreSQL database, allowing users to continue their chats seamlessly.

stage3

Specifically, we store the chat ID, chat name, and file path of each conversation in PostgreSQL. Whenever the chatbot is reopened, it automatically retrieves the previous chat history, providing a smoother user experience.

By separating responsibilities—Streamlit for the frontend, FastAPI for backend logic, and PostgreSQL for data storage—we ensure a flexible and maintainable architecture. Each component can be updated or replaced independently, making it easier to extend functionality without affecting the overall system. Additionally, this structure lays the foundation for a smooth transition to cloud deployment in future stages.

<img src="/assets/St-3.png" width="650"/>

---

Stage 4 - Chatbot with Chat History

A RAG (Retrieval-Augmented Generation) chatbot using Streamlit and FastAPI. At this stage, we introduce the ability for users to upload PDF files in addition to regular chatting. This allows them to ask questions specifically about the content of those documents.

Under the hood, the system uses a vector store (Chroma) to retrieve the most relevant context from uploaded PDFs. This retrieval step enhances the chatbot’s ability to provide accurate, context-aware answers, bridging the gap between simple conversation and document-focused queries.

This enhancement integrates seamlessly with our existing setup—Streamlit for the user interface, FastAPI for business logic, and PostgreSQL for data storage—while laying the foundation for further expansion.

<img src="/assets/St-4.png" width="650"/>

---

Project Stage 5: Moving to Azure VM Manually

At this stage, we will move our application to an Azure VM. We’ll create a new VM and deploy our databases, frontend, and backend services on it. Additionally, we will manually set up the following components: an Azure network security group, an Azure Virtual Network, a public IP address, a subnet, a disk, and a network interface. Note that we will not use Infrastructure as Code (IaC) at this stage; everything will be set up manually.

<img src="/assets/St-5.png" width="650"/>

---

Project Stage 6: Postgres and Blob Storage on Azure

Based on Stage 5, we are adding two new resources to the infrastructure: an Azure Database for PostgreSQL server and Azure Blob Storage. Instead of running PostgreSQL on the VM, we’ll use the Azure Database for PostgreSQL server for data storage, and files will be stored in Azure Blob Storage.

<img src="/assets/St-6.png" width="650"/>

---

Project Stage 6.1: Application Gateway and VMSS on Azure

Based on Stage 6, we are adding two new resources to the infrastructure: an Azure Application Gateway and a Virtual Machine Scale Set (VMSS). The Azure Application Gateway will redirect traffic to the VMSS, which will host our application.

At stage, the VM is only used for deploying ChromaDB.

The frontend and backend services will be deployed on the VMSS. In order to do this, we need to create a new image from a VM and use it to create a VMSS. The VM will be deleted, but the image will be kept. This image should have the frontend and backend services set up and running.

<img src="/assets/St-6.1.png" width="650"/>

---

Project Stage 5: Moving to Azure VM with Terraform
At this stage, we will use Terraform

<img src="/assets/St-5.png" width="650"/>

---

Project Stage 6: Postgres and Blob Storage on Azure with Terraform

Based on Stage 5, we are adding two new scripts: db.tf and storage.tf to provision an Azure Database for PostgreSQL server and Azure Blob Storage. Instead of running PostgreSQL on the VM, we’ll use the Azure Database for PostgreSQL server for data storage, and files will be stored in Azure Blob Storage.

Once the infrastructure is provisioned with Terraform, the VM, database, CICD pipeline, and application should be set up manually.

In the end, you should be able to access the application via the VM’s public IP address, with data stored in the Azure Database for PostgreSQL server and files stored in Azure Blob Storage.

<img src="/assets/St-6.png" width="650"/>

---

Project Stage 6.1: Application Gateway and VMSS on Azure with Terraform


Based on Stage 6, we are adding two new scripts: VMSS.tf and application-gateway.tf to provision a Virtual Machine Scale Set (VMSS) and an Azure Application Gateway. Additionally, the network.tf script will be updated to add a new subnet, a security group, and the necessary security rule. The Application Gateway will redirect traffic to the VMSS, which will host our application.

Once Terraform has provisioned the infrastructure, the VM, database, CI/CD pipeline, and application will be set up manually.

In the end, you should be able to access the application via the Application Gateway's public IP address, with data stored in the Azure Database for PostgreSQL server and files stored in Azure Blob Storage.

<img src="/assets/St-6.1.png" width="650"/>

---

Project Stage 6.5: Azure Key Vault on Azure

Based on Stage 6.1, we are adding Azure Key Vault to the infrastructure. The Azure Key Vault will store the secrets and environment variables for the application. The secrets and environment variables will be retrieved from the Key Vault during the application deployment process.

The other infrastructure components are the same as stage 6.1.

In the end, you should be able to access the application via the Application Gateway's public IP address, with data stored in the Azure Database for PostgreSQL server and files stored in Azure Blob Storage.

<img src="/assets/St-6.5.png" width="650"/>

---

Project Stage 7: Azure Function App

Based on Stage 6.5, we are replacing the Azure Application Gateway and VMSS with Azure Function App. The Azure Function App will host the backend of the application. The VM will be used to host the frontend and ChromaDB. At this stage, we should create and setup infrastructure in this diagram manually.

The GitHub Actions workflow should be updated to deploy the backend to the Azure Function App.

In the end, you should be able to access the application via the VM's public IP address, with data stored in the Azure Database for PostgreSQL server and files stored in Azure Blob Storage.

<img src="/assets/St-7.png" width="650"/>


---

Project Stage 8: Azure Cosmos DB

Based on Stage 7, we are adding an Azure Cosmos DB to the infrastructure. The Azure Cosmos DB will store the chat history of the application. At this stage, we should create and setup infrastructure in this diagram manually. The primary key of the Cosmos DB should be stored in the Key Vault.

In the end, you should be able to access the application via the VM's public IP address, with data stored in the Azure Database for PostgreSQL server, files stored in Azure Blob Storage, and chat history stored in Azure Cosmos DB.

<img src="/assets/St-8.png" width="650"/>
