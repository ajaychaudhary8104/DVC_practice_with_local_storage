# DVC Practice with Local Storage

A practice project for learning **Data Version Control (DVC)** with local storage backend. This project demonstrates how to set up DVC for data versioning, track changes across multiple versions, and manage data pipelines using Git and DVC together.

## 📋 Overview

This project showcases:
- **Data versioning** with DVC (Data Version Control)
- **Local storage** setup as a remote backend (S3-like structure)
- **Python data generation** with Pandas
- **Git and DVC integration** for complete version control workflow
- **Multi-version data tracking** from V1 to V3

## 🛠️ Prerequisites

- **Python 3.x** installed
- **Git** installed and configured
- **DVC** package installed

### Installation

Install the required packages:

```bash
pip install dvc pandas
```

## 📁 Project Structure

```
DVC_practice_with_local_storage/
├── mycode.py              # Main Python script that generates sample data
├── data/                  # Data directory (tracked by DVC)
│   └── sample_data.csv    # Generated sample dataset
├── s3/                    # Local S3 remote storage
│   └── files/md5/        # Content-addressable storage structure
├── data.dvc              # DVC file tracking data directory
├── .dvc/                 # DVC configuration directory
├── .git/                 # Git repository
├── .gitignore            # Git ignore rules
├── LICENSE               # MIT License
├── projectflow.txt       # Project workflow documentation
└── README.md             # This file
```

## 🚀 Quick Start

### Step 1: Clone and Setup

```bash
# Create git repo (already done in this project)
git clone <repo-url>
cd DVC_practice_with_local_storage
```

### Step 2: Initialize DVC

```bash
# Initialize DVC
dvc init

# Create local S3 directory for remote storage
mkdir s3

# Add remote storage
dvc remote add -d myremote s3
```

### Step 3: Track Data with DVC

```bash
# Add data directory to DVC tracking
dvc add data/

# Stop Git from tracking data directory
git rm -r --cached 'data'
git commit -m "stop tracking data"

# Commit and push to remote
dvc commit
dvc push

# Commit changes to Git
git add .gitignore data.dvc
git commit -m "Initial data version (V1)"
git push
```

## 📝 Data Versions

This project tracks three versions of sample data:

### V1 - Initial Data
- Alice (25, New York)
- Bob (30, Los Angeles)
- Charlie (35, Chicago)

### V2 - Added GF1
- All V1 entries plus
- GF1 (20, City1)

### V3 - Added GF2
- All V2 entries plus
- GF2 (30, City2)

## 🔄 Workflow for Adding New Data Versions

1. **Modify** `mycode.py` to add/change data
2. **Run** the script to regenerate CSV:
   ```bash
   python mycode.py
   ```
3. **Check** DVC status:
   ```bash
   dvc status
   ```
4. **Commit and push** data changes:
   ```bash
   dvc commit
   dvc push
   git add data.dvc
   git commit -m "Update data to version X"
   git push
   ```

## 📊 Key Files Explained

- **mycode.py**: Generates a sample DataFrame with Name, Age, and City columns, then saves it as CSV
- **data.dvc**: Metadata file for tracking the `data/` directory
- **s3/**: Local remote storage directory (simulates S3 bucket)
- **projectflow.txt**: Detailed step-by-step workflow documentation

## 🔍 Common DVC Commands

```bash
# Check DVC status
dvc status

# View data file changes
dvc diff

# Fetch data from remote
dvc pull

# Push data to remote
dvc push

# Remove local cache
dvc cache remove
```

## 📚 Learn More

- [DVC Official Documentation](https://dvc.org/doc)
- [DVC Getting Started Guide](https://dvc.org/doc/start)
- [Git-based Workflows](https://dvc.org/doc/user-guide/basic-concepts/remote)

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

Copyright (c) 2026 AJAY CHAUDHARY

## 🤝 Contributing

Feel free to fork, modify, and experiment with different DVC configurations and workflows!

---

**Note**: This is a practice project designed for learning DVC concepts. For production use, consider using cloud-based remote storage (AWS S3, Azure Blob Storage, etc.)