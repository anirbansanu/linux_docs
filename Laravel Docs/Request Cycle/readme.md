```mermaid
graph TD
    A[Request Lifecycle] --> B[Introduction]
    B --> C[Lifecycle Overview]
    C --> D[First Steps]
    D --> E[HTTP / Console Kernels]
    E --> F[Service Providers]
    F --> G[Routing]
    G --> H[Finishing Up]
    
    subgraph Detailed Lifecycle Overview
        direction TB
        D --> I[public/index.php]
        I --> J[Load Composer Autoloader]
        J --> K[Retrieve Laravel Application Instance from bootstrap/app.php]
        K --> L[Create Application / Service Container]
        L --> M[Determine Request Type]
        M --> N[HTTP Request -> HTTP Kernel]
        M --> O[Console Request -> Console Kernel]
        N --> P[Run Bootstrappers]
        P --> Q[Configure Error Handling, Logging, Environment]
        Q --> R[Process Middleware Stack]
        R --> S[Handle Request -> Return Response]
    end
    
    subgraph Detailed Service Providers
        direction TB
        F --> T[Load Service Providers]
        T --> U[Instantiate Providers]
        U --> V[Call register Method on Providers]
        V --> W[Call boot Method on Providers]
        W --> X[Bootstrap and Configure Framework Components]
    end
    
    subgraph Detailed Routing
        direction TB
        G --> Y[Router Dispatch Request]
        Y --> Z[Route to Controller or Route]
        Z --> AA[Run Route Specific Middleware]
        AA --> AB[Execute Route / Controller Method]
        AB --> AC[Return Response]
    end
    
    subgraph Detailed Finishing Up
        direction TB
        H --> AD[Response Travels Back through Middleware]
        AD --> AE[Modify / Examine Outgoing Response]
        AE --> AF[HTTP Kernel's handle method]
        AF --> AG[Application Instance handleRequest]
        AG --> AH[send method on Response]
        AH --> AI[Send Response to Browser]
    end
```