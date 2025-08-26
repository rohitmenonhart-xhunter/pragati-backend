# Pragati Innovation Suite - Complete Setup Guide

## 🎯 Overview

This guide provides step-by-step instructions for setting up the Pragati Innovation Suite development environment with Conda and Python 3.11.

**⚠️ NOTICE: This is proprietary software owned by Stacia Corp. Unauthorized access, use, or distribution is strictly prohibited.**

## 📋 Prerequisites

### Required Software
- **Conda** (Anaconda or Miniconda) - [Download](https://docs.conda.io/en/latest/miniconda.html)
- **Git** - [Download](https://git-scm.com/downloads)
- **Python 3.11** (will be installed via Conda)

### Required Accounts & API Keys
1. **OpenAI Account** - [Sign up](https://platform.openai.com/signup)
2. **Google Cloud Account** (for Gemini) - [Sign up](https://cloud.google.com/)
3. **MongoDB** - Local installation or [MongoDB Atlas](https://www.mongodb.com/atlas)
4. **AWS Account** (optional) - For S3 and SES services

---

## 🚀 Step-by-Step Installation

### Step 1: Clone the Repository
```bash
git clone https://github.com/rohitmenonhart-xhunter/pragati-backend.git
cd pragati-backend
```

### Step 2: Create Conda Environment
```bash
# Create environment with Python 3.11
conda create -n pragati-backend python=3.11 -y

# Activate the environment
conda activate pragati-backend

# Verify Python version
python --version
# Should output: Python 3.11.x
```

### Step 3: Install Dependencies

#### Core Dependencies via Conda (Recommended)
```bash
# Install core packages from conda-forge
conda install -c conda-forge flask pymongo boto3 pyjwt bcrypt python-dotenv -y

# Install additional packages
conda install -c conda-forge matplotlib numpy requests -y
```

#### Remaining Dependencies via Pip
```bash
# Install AI/ML packages and other dependencies
pip install -r requirements.txt
```

### Step 4: Environment Configuration

#### Copy Environment Template
```bash
cp .env.example .env
```

#### Edit .env File
Open `.env` file and configure the following:

```env
# AI API Keys
OPENAI_API_KEY=sk-your-openai-api-key-here
GEMINI_API_KEY=your-gemini-api-key-here

# Database Configuration
MONGO_URI=mongodb://localhost:27017/pragati
MONGO_DB_NAME=pragati

# JWT Configuration
JWT_SECRET=your-super-secret-jwt-key-here

# AWS Configuration (Optional)
AWS_ACCESS_KEY_ID=your-aws-access-key
AWS_SECRET_ACCESS_KEY=your-aws-secret-key
AWS_REGION=us-east-1
AWS_S3_BUCKET=your-s3-bucket-name

# Application Configuration
PRAGATI_APP_ID=pragati-innovation-suite
```

---

## 🔑 API Keys Setup

### OpenAI API Key
1. Go to [OpenAI Platform](https://platform.openai.com/api-keys)
2. Sign in or create an account
3. Click "Create new secret key"
4. Copy the key and add to your `.env` file

### Google Gemini API Key
1. Go to [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Sign in with your Google account
3. Click "Create API Key"
4. Copy the key and add to your `.env` file

### MongoDB Setup
Choose one of the following options:

#### Option A: Local MongoDB
```bash
# Install MongoDB locally
# Windows: Download from https://www.mongodb.com/try/download/community
# macOS: brew install mongodb-community
# Linux: Follow official installation guide

# Start MongoDB service
# Windows: Start as Windows service
# macOS/Linux: mongod --config /usr/local/etc/mongod.conf
```

#### Option B: MongoDB Atlas (Cloud)
1. Sign up at [MongoDB Atlas](https://www.mongodb.com/atlas)
2. Create a free cluster
3. Get connection string and add to `.env` file

---

## ✅ Verification

### Test Installation
```bash
# Ensure environment is activated
conda activate pragati-backend

# Test Python imports
python -c "import flask, pymongo, openai; print('✅ Core dependencies imported successfully')"

# Test AI Logic V2 loading
python -c "from app.ai_logic_v2 import EvaluationFramework; print('✅ V2 AI Logic loaded successfully')"

# Verify parameter count
python -c "from app.ai_logic_v2 import EvaluationFramework; f=EvaluationFramework(); print(f'✅ Total parameters: {sum(len(s) for p in f.SUB_PARAMETER_WEIGHTS.values() for s in p.values())}')"
```

### Start the Application
```bash
# Start Flask development server
python -m flask run

# Expected output:
# * Running on http://127.0.0.1:8000
# * Debug mode: off
```

### Test API Endpoint
Open browser or use curl:
```bash
curl http://127.0.0.1:8000/
```

---

## 🔧 Troubleshooting

### Common Issues

#### Issue 1: ModuleNotFoundError
```bash
# Make sure environment is activated
conda activate pragati-backend

# Reinstall dependencies
pip install -r requirements.txt
```

#### Issue 2: SSL Certificate Issues
```bash
# Clear problematic environment variables
unset CURL_CA_BUNDLE
unset REQUESTS_CA_BUNDLE

# Reinstall with conda
conda install -c conda-forge requests urllib3
```

#### Issue 3: MongoDB Connection Error
```bash
# Check MongoDB is running
# For local: Check service status
# For Atlas: Verify connection string and network access
```

#### Issue 4: API Key Issues
```bash
# Verify .env file is in project root
# Check API keys are correctly formatted
# Ensure no extra spaces or quotes
```

### Environment Reset
If you need to start fresh:
```bash
# Remove environment
conda deactivate
conda env remove -n pragati-backend

# Recreate environment
conda create -n pragati-backend python=3.11 -y
conda activate pragati-backend

# Reinstall dependencies
conda install -c conda-forge flask pymongo boto3 pyjwt bcrypt python-dotenv matplotlib numpy requests -y
pip install -r requirements.txt
```

---

## 🚀 Development Workflow

### Daily Development
```bash
# Activate environment
conda activate pragati-backend

# Start development server
python -m flask run

# In another terminal (for testing)
python -c "from app.ai_logic_v2 import validate_idea; print('Testing V2...')"
```

### Running Accuracy Tests
```bash
# Run startup accuracy comparison
python real_startup_accuracy_test.py

# Run AI logic comparison
python ai_logic_openai_comparison.py
```

### Code Testing
```bash
# Test AI logic loading
python -c "from app.ai_logic import validate_idea as v1; from app.ai_logic_v2 import validate_idea as v2; print('Both versions loaded successfully')"
```

---

## 📚 Additional Resources

- [Flask Documentation](https://flask.palletsprojects.com/)
- [Conda User Guide](https://docs.conda.io/projects/conda/en/latest/user-guide/)
- [OpenAI API Documentation](https://platform.openai.com/docs)
- [Google Gemini API Documentation](https://ai.google.dev/docs)
- [MongoDB Documentation](https://docs.mongodb.com/)

---

## 🤝 Support

If you encounter any issues during setup:

1. Check this troubleshooting guide
2. Verify all prerequisites are installed
3. Ensure API keys are correctly configured
4. Check the [GitHub Issues](https://github.com/rohitmenonhart-xhunter/pragati-backend/issues) page

---

**Happy coding! 🎉**
