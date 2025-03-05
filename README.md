I'll update the license section and clarify the architecture regarding storage.

# **🌤️ OpenWeatherMap Data Pipeline Engineering Project**

<div align="center">
    <a href="https://github.com/yourusername/weather-data-pipeline/">
        <img src="https://img.shields.io/badge/Visit%20Weather%20Pipeline-brightgreen?style=for-the-badge&logo=github" alt="Visit Weather Pipeline"/>
    </a>
</div>

![Weather Data Pipeline](/images/weather_pipeline.png)

---

## **📄 Overview**
The **OpenWeatherMap Data Pipeline Engineering Project** is a comprehensive data engineering solution that collects, processes, and analyzes weather data from the OpenWeatherMap API. It demonstrates a complete ETL (Extract, Transform, Load) pipeline with monitoring, visualization, and multiple deployment options, designed to deliver actionable weather insights across multiple cities.

```mermaid
flowchart LR
    User([User])
    API[Weather API]
    ETL[ETL Pipeline]
    DB[(Storage)]
    Monitor[Monitoring]
    Insight[Analytics]
    
    User --> API
    API --> ETL
    ETL --> DB
    DB --> Insight
    ETL <--> Monitor
    Insight --> User
    
    style API fill:#93c5fd,stroke:#2563eb,stroke-width:2px
    style ETL fill:#fde68a,stroke:#d97706,stroke-width:2px
    style Monitor fill:#d1fae5,stroke:#059669,stroke-width:2px
    style Insight fill:#fbcfe8,stroke:#db2777,stroke-width:2px
```

---

### Architecture Flow
```mermaid
flowchart TD
    classDef application fill:#3178C6,stroke:#13233A,color:white
    classDef storage fill:#3B873A,stroke:#0A2F0A,color:white
    classDef processing fill:#E535AB,stroke:#A1145A,color:white
    classDef monitoring fill:#412991,stroke:#231648,color:white
    classDef client fill:#2C5BB4,stroke:#153A78,color:white
    classDef security fill:#DD0031,stroke:#A10000,color:white

    Client[Client Applications]:::client
    
    subgraph APILayer["API Layer"]
        Python[Python Application]:::application
        Config[Configuration]:::security
        Validation[Input Validation]:::security
    end
    
    subgraph StorageLayer["Storage Layer"]
        FileSystem[Local File System]:::storage
        subgraph DataStructure["Data Structure"]
            Raw[Raw Data]:::storage
            Processed[Processed Data]:::storage
            Output[Analysis Output]:::storage
        end
    end
    
    subgraph ProcessingLayer["Processing Layer"]
        Extract[Data Extraction]:::processing
        Transform[Data Transformation]:::processing
        Load[Data Loading]:::processing
        Analyze[Data Analysis]:::processing
    end
    
    subgraph MonitoringLayer["Monitoring Layer"]
        Prometheus[Prometheus]:::monitoring
        Grafana[Grafana]:::monitoring
        Metrics[Performance Metrics]:::application
    end
    
    Client --> Python
    Python --> Config
    Config --> Validation
    
    Validation --> Extract
    Extract --> Raw
    Raw --> Transform
    Transform --> Processed
    Processed --> Load
    Processed --> Analyze
    Analyze --> Output
    
    Python --> Metrics
    Metrics --> Prometheus
    Prometheus --> Grafana
    
    Python --> Client
```

---

## **Table of Contents**
1. [🎯 Key Features](#-key-features)
2. [🔧 Technology Stack](#-technology-stack)
3. [📝 Project Structure](#-project-structure)
4. [🚀 Getting Started](#-getting-started)
5. [🔄 Processing Pipeline](#-processing-pipeline)
6. [📊 Data Analysis](#-data-analysis)
7. [🛠️ Deployment Options](#-deployment-options)
8. [🔍 Monitoring](#-monitoring)
9. [📚 References](#-references)
10. [📜 License](#-license)

---

## **🎯 Key Features**
- **☁️ Automated Weather Data Collection**
  - Multi-city weather data extraction
  - Configurable sampling frequency
  - Resilient API connectivity with retry logic

- **⚙️ Robust Data Processing**
  - Data cleaning and normalization
  - Outlier detection and handling
  - Derived metrics calculation

- **📊 Comprehensive Analytics**
  - City-to-city weather comparisons
  - Temperature trend analysis
  - Weather pattern visualization

- **☸️ Enterprise-Grade Infrastructure**
  - Docker containerization
  - Kubernetes orchestration
  - Multiple deployment options (local, EC2, Airflow)

---

## **🔧 Technology Stack**

![Python](https://img.shields.io/badge/python-3.12.8+-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)

```mermaid
flowchart TD
    subgraph Core["Core Technologies"]
        Python["Python 3.12.8+"]
        Pandas["Pandas"]
        Matplotlib["Matplotlib"]
    end
    
    subgraph Deployment["Deployment Tools"]
        Docker["Docker"]
        K8s["Kubernetes"]
        Airflow["Apache Airflow"]
    end
    
    subgraph Monitoring["Monitoring Stack"]
        Prometheus["Prometheus"]
        Grafana["Grafana"]
    end
    
    subgraph API["External APIs"]
        Weather["OpenWeatherMap API"]
    end
    
    Python --> Weather
    Python --> Pandas
    Python --> Matplotlib
    Python --> Docker
    Docker --> K8s
    K8s --> Airflow
    Python --> Prometheus
    Prometheus --> Grafana
    
    style Core fill:#93c5fd,stroke:#2563eb,stroke-width:2px
    style Deployment fill:#fde68a,stroke:#d97706,stroke-width:2px
    style Monitoring fill:#d1fae5,stroke:#059669,stroke-width:2px
    style API fill:#fbcfe8,stroke:#db2777,stroke-width:2px
```

**Core Dependencies:**
- **Python**: Primary development language
- **Pandas**: Data manipulation and analysis
- **Matplotlib**: Visualization and plotting
- **PyYAML**: Configuration handling
- **Requests**: API communication
- **SQLite**: Local database storage
- **Prometheus-client**: Metrics instrumentation

---

## **📝 Project Structure**
```plaintext
weather_data_pipeline/
├── README.md                     # Project documentation
├── config/
│   └── config.yaml               # Configuration parameters
├── data/
│   ├── raw/                      # Raw data storage
│   ├── processed/                # Processed data storage
│   └── output/                   # Final analysis output
├── logs/                         # Log files
├── requirements.txt              # Python dependencies
├── src/
│   ├── __init__.py
│   ├── extract.py                # Data extraction module
│   ├── transform.py              # Data transformation module
│   ├── load.py                   # Data loading module
│   ├── analyze.py                # Data analysis module
│   └── utils.py                  # Utility functions
├── main.py                       # Main execution script
├── Dockerfile                    # Docker configuration
├── docker-compose.yml            # Docker Compose setup
├── airflow/                      # Airflow DAG definitions
├── kubernetes/                   # Kubernetes deployment files
├── monitoring/                   # Prometheus and Grafana setup
└── .github/workflows/            # GitHub Actions CI/CD
```

---

## **🚀 Getting Started**

### 1. Clone the Repository
```bash
git clone https://github.com/yourusername/weather-data-pipeline.git
cd weather-data-pipeline
```

### 2. Set Up Environment
```bash
# Create and activate a virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Create .env file with your API key
echo "API_KEY=your_openweathermap_api_key" > .env
```

### 3. Run the Pipeline
```bash
# Run the complete pipeline
python main.py

# Run specific phases
python main.py --skip-extract     # Use existing raw data
python main.py --skip-transform   # Use existing processed data
python main.py --skip-analyze     # Skip analysis phase
python main.py --skip-load        # Skip loading phase
```

### 4. View Results
- Raw data: `data/raw/`
- Processed data: `data/processed/`
- Analysis and visualizations: `data/output/`
- Logs: `logs/pipeline.log`

---

## **🔄 Processing Pipeline**

```mermaid
graph TD
    A[Input Configuration] --> B[Data Extraction]
    B --> C[Data Transformation]
    C --> D[Data Loading]
    C --> E[Data Analysis]
    E --> F[Visualization]
    F --> G[Results]
```

```mermaid
sequenceDiagram
    participant Main as Main Script
    participant Extract as Extractor
    participant Transform as Transformer
    participant Load as Loader
    participant Analyze as Analyzer
    participant API as OpenWeatherMap API
    
    Main->>Extract: Initialize Extraction
    Extract->>API: Request Weather Data
    API-->>Extract: Return Weather Data
    Extract->>Extract: Save Raw Data
    Extract-->>Main: Return Extracted Data
    
    Main->>Transform: Initialize Transformation
    Transform->>Transform: Load Raw Data
    Transform->>Transform: Clean and Process Data
    Transform->>Transform: Save Processed Data
    Transform-->>Main: Return Transformed Data
    
    Main->>Load: Initialize Loading
    Load->>Load: Load Processed Data
    Load->>Load: Export to Different Formats
    Load-->>Main: Return Loading Status
    
    Main->>Analyze: Initialize Analysis
    Analyze->>Analyze: Load Processed Data
    Analyze->>Analyze: Calculate Statistics
    Analyze->>Analyze: Generate Visualizations
    Analyze->>Analyze: Save Results
    Analyze-->>Main: Return Analysis Results
```

---

## **📊 Data Analysis**

```mermaid
mindmap
    root((Weather Analysis))
        City Comparisons
            Temperature Ranges
            Humidity Levels
            Wind Speed Patterns
        Temporal Analysis
            Daily Fluctuations
            Trend Detection
        Weather Conditions
            Condition Distribution
            Pattern Recognition
        Correlations
            Temperature-Humidity
            Weather-Wind Relationships
```

The pipeline performs comprehensive analysis of weather data:
1. **City Comparisons**: Compare weather metrics across different cities
2. **Temperature Analysis**: Track temperature trends and variations
3. **Humidity Patterns**: Analyze humidity levels and correlations
4. **Wind Analysis**: Examine wind speed and direction patterns
5. **Weather Conditions**: Categorize and analyze weather condition distributions

Sample visualizations include:
- Temperature comparison charts
- Time-series temperature trend graphs
- Weather condition distribution pie charts
- Temperature-humidity correlation plots
- Wind speed distribution box plots

---

## **🛠️ Deployment Options**

### Local Docker Deployment

```bash
# Build and run with Docker Compose
docker-compose up --build
```

Access:
- Prometheus: http://localhost:9090
- Grafana: http://localhost:3000 (admin/admin)

### Kubernetes Deployment with Minikube

```bash
# Start Minikube
minikube start

# Create Secret for API Key
kubectl create secret generic weather-pipeline-secrets \
  --from-literal=API_KEY=your_openweathermap_api_key

# Apply the configuration
kubectl apply -f kubernetes/deployment.yaml
```

### Airflow (Local)

```bash
# Install Airflow
pip install apache-airflow

# Initialize Airflow database
airflow db init

# Create a user
airflow users create \
  --username admin \
  --password admin \
  --firstname Admin \
  --lastname User \
  --role Admin \
  --email admin@example.com

# Copy DAG file to Airflow DAGs directory
mkdir -p ~/airflow/dags
cp airflow/weather_pipeline_dag.py ~/airflow/dags/

# Start Airflow
airflow webserver --port 8080
airflow scheduler
```

Access Airflow UI: http://localhost:8080

### EC2 Deployment with GitHub Actions CI/CD

```mermaid
flowchart TD
    subgraph Development["Local Development"]
        Develop[Develop & Test]
        Commit[Commit Changes]
        Push[Push to GitHub]
    end
    
    subgraph Deployment["Deployment Process"]
        GitHub[GitHub Repository]
        Actions[GitHub Actions]
        EC2[EC2 Instance]
        Setup[Setup & Configuration]
        Run[Run Application]
    end
    
    Develop --> Commit
    Commit --> Push
    Push --> GitHub
    GitHub --> Actions
    Actions --> EC2
    EC2 --> Setup
    Setup --> Run
    
    style Development fill:#d1fae5,stroke:#059669,stroke-width:2px
    style Deployment fill:#93c5fd,stroke:#2563eb,stroke-width:2px
```

The included GitHub Actions workflow automatically tests, builds, and deploys the pipeline on push to the main branch.

---

## **🔍 Monitoring**

### Prometheus Metrics

The pipeline exposes metrics on port 8000, including:
- Pipeline execution counts and durations
- Data extraction successes and failures
- Processing counts and times
- Error rates and outliers

### Grafana Dashboard

A pre-configured dashboard is included in `monitoring/grafana-dashboard.json` showing:
- Pipeline success/failure rates
- Data processing volumes
- API performance metrics
- Execution times

Sample Grafana dashboard:

```mermaid
graph TD
    subgraph Dashboard["Weather Pipeline Dashboard"]
        subgraph row1["Pipeline Performance"]
            A[Pipeline Runs] --- B[Pipeline Failures]
            C[Extraction Success Rate] --- D[API Response Time]
        end
        
        subgraph row2["Data Statistics"]
            E[Records Processed] --- F[Data Points Extracted]
            G[Outliers Detected] --- H[Processing Time]
        end
        
        subgraph row3["Weather Metrics"]
            I[Average Temperature by City] --- J[Weather Condition Distribution]
            K[Temperature Trends] --- L[Humidity Correlation]
        end
    end
```

---

## **📚 References**
- [Pandas Documentation](https://pandas.pydata.org/docs/)
- [Matplotlib Documentation](https://matplotlib.org/stable/contents.html)
- [OpenWeatherMap API Documentation](https://openweathermap.org/api)
- [Docker Documentation](https://docs.docker.com/)
- [Kubernetes Documentation](https://kubernetes.io/docs/home/)
- [Prometheus Documentation](https://prometheus.io/docs/introduction/overview/)

---

## **📜 License**
**Copyright © 2025 Fahmi Zainal**

All rights reserved. This project and its contents are proprietary and confidential. Unauthorized copying, distribution, or modification of this software, via any medium, is strictly prohibited. For licensing inquiries, please contact the project maintainer.