# Research Service

Comprehensive research and data analysis platform for managing research projects, data collection, and report generation.

## 📁 Structure

```
research/
├── frontend/
│   ├── src/
│   │   ├── components/    # Data visualization, tables
│   │   ├── pages/         # Projects, datasets, reports
│   │   ├── services/
│   │   ├── store/
│   │   └── styles/
│   ├── Dockerfile
│   └── package.json
│
├── backend/
│   ├── src/
│   │   ├── controllers/
│   │   ├── services/      # Analysis engines
│   │   ├── models/
│   │   ├── routes/
│   │   ├── analysis/      # Statistical analysis
│   │   ├── processors/    # Data processing
│   │   ├── workers/       # Background jobs
│   │   └── utils/
│   ├── Dockerfile
│   └── package.json
│
├── database/
│   ├── migrations/
│   └── schemas/
│       └── research_schema.sql
│
└── docker-compose.yml
```

## 🚀 Quick Start

```bash
# Start services
docker-compose up -d

# Install dependencies
pnpm install

# Run backend
cd backend && pnpm dev

# Run frontend
cd frontend && pnpm dev
```

Access at `http://localhost:5005`

## 🎯 Features

- **Research Project Management**: Organize and track research initiatives
- **Data Collection**: Multiple data collection methods
- **Statistical Analysis**: Advanced statistical analysis tools
- **Data Visualization**: Interactive charts and graphs
- **Report Generation**: Automated report creation
- **Collaboration**: Team-based research workflows
- **Version Control**: Track research iterations

## 📊 Database Schema

### Research Projects Table
```sql
CREATE TABLE research_projects (
  id UUID PRIMARY KEY,
  title VARCHAR(255),
  description TEXT,
  owner_id UUID REFERENCES users(id),
  status ENUM('planning', 'active', 'completed', 'archived'),
  created_at TIMESTAMP,
  updated_at TIMESTAMP
);
```

### Datasets Table
```sql
CREATE TABLE datasets (
  id UUID PRIMARY KEY,
  project_id UUID REFERENCES research_projects(id),
  name VARCHAR(255),
  description TEXT,
  data_type ENUM('numerical', 'categorical', 'text', 'mixed'),
  record_count INTEGER,
  created_at TIMESTAMP
);
```

### Analysis Results Table
```sql
CREATE TABLE analysis_results (
  id UUID PRIMARY KEY,
  dataset_id UUID REFERENCES datasets(id),
  analysis_type VARCHAR(100),
  results JSONB,
  created_at TIMESTAMP
);
```

## 🔌 API Endpoints

### Projects
- `GET /api/projects` - List projects
- `POST /api/projects` - Create project
- `GET /api/projects/:id` - Get project details
- `PATCH /api/projects/:id` - Update project
- `DELETE /api/projects/:id` - Delete project

### Datasets
- `POST /api/datasets/upload` - Upload dataset
- `GET /api/datasets` - List datasets
- `GET /api/datasets/:id` - Get dataset
- `POST /api/datasets/:id/analyze` - Analyze dataset
- `DELETE /api/datasets/:id` - Delete dataset

### Analysis
- `POST /api/analysis/descriptive` - Descriptive statistics
- `POST /api/analysis/correlation` - Correlation analysis
- `POST /api/analysis/regression` - Regression analysis
- `POST /api/analysis/clustering` - Clustering analysis
- `GET /api/analysis/:id/results` - Get analysis results

### Reports
- `GET /api/reports` - List reports
- `POST /api/reports/generate` - Generate report
- `GET /api/reports/:id` - Download report
- `DELETE /api/reports/:id` - Delete report

## 🔧 Configuration

```env
# Analysis
MAX_DATASET_SIZE=1000000
ANALYSIS_TIMEOUT=3600
DEFAULT_ANALYSIS_TYPE=descriptive

# Processing
DATA_PROCESSING_ENGINE=python
STATISTICS_LIBRARY=scipy

# Storage
DATASET_STORAGE_PATH=/datasets
EXPORT_FORMATS=csv,json,xlsx,parquet
```

## 🧪 Testing

```bash
# Run tests
pnpm test

# Run with specific test file
pnpm test -- --file=analysis.test.ts
```

## 📚 API Documentation

Available at `http://localhost:3005/api/docs`

## 🚢 Deployment

```bash
docker build -t agentics-research:latest .
docker push agentics-research:latest
kubectl apply -f k8s/
```

---

**Part of Agentics Labs Platform**
