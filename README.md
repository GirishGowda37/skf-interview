# SKF Products Assistant

##  Overview
This is a full-stack solution that allows users to ask natural language questions about SKF products. It uses:

-  **Azure Functions (.NET 8)** as the backend
-  **Azure OpenAI** to extract product codes and generate accurate answers
-  **React** frontend for a user-friendly chat interface
-  JSON-based product data located in the `Data` folder


## Prerequisites

### Backend (Azure Functions)
- [.NET SDK 8](https://dotnet.microsoft.com/en-us/download/dotnet/8.0)
- [Azure Functions Core Tools v4+](https://learn.microsoft.com/en-us/azure/azure-functions/functions-run-local)
- A valid Azure OpenAI resource with:
  - `AZURE_OPENAI_KEY`
  - `AZURE_OPENAI_ENDPOINT`
  - `AZURE_OPENAI_DEPLOYMENT`

### Frontend (React)
- Node.js v18+
- npm or yarn

##  Running the Project

### 1.  Backend (Azure Function)

```bash
cd FunctionApp
dotnet restore
func start
```

Ensure `local.settings.json` includes:

```json
{
  "IsEncrypted": false,
  "Values": {
    "AzureWebJobsStorage": "UseDevelopmentStorage=true",
    "FUNCTIONS_WORKER_RUNTIME": "dotnet",
    "AZURE_OPENAI_KEY": "<your-key>",
    "AZURE_OPENAI_ENDPOINT": "https://<your-resource>.openai.azure.com",
    "AZURE_OPENAI_DEPLOYMENT": "<deployment-name>"
  }
}
```

Place your product data in `/FunctionApp/Data/`, e.g.:

- `6205.json`
- `6025 N.json`

### 2.  Frontend (React)

```bash
cd SKFClient
npm install
npm start
```

This opens your React app at:  
 `http://localhost:3000`

##  Testing

1. Go to `http://localhost:3000`
2. Try asking:
   - _“What is the width of 6205?”_
3. The app will:
   - Send the query to the backend
   - Backend extracts product names
   - Loads corresponding JSON files
   - Sends to Azure OpenAI
   - Returns a structured answer


##  Deployment (Optional)

- Backend: Deploy `SKFInterviewOpenAI` to Azure Functions
- Frontend: Deploy `SKF-Client` to Azure Static Web
