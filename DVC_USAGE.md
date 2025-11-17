# DVC (Data Version Control) Setup Guide

## What is DVC?

DVC helps track large files (datasets, models) using Git-like commands without storing them in Git. Instead, it stores lightweight `.dvc` files that point to the actual data stored elsewhere.

## Setup Complete ✓

DVC has been initialized in this repository. The following directories are ready to be tracked:

- `data/` - Datasets
- `models/` - Trained models

## Common DVC Commands

### Track New Data/Model Files

```bash
# Track a specific data file
dvc add data/sentiment140_sampled_200k.csv

# Track entire models directory
dvc add models/bertweet_sentiment_finetuned

# Track raw dataset
dvc add data/training.1600000.processed.noemoticon.csv
```

After running `dvc add`, Git will show new `.dvc` files. **Commit these** to Git:

```bash
git add data/*.dvc models/*.dvc .gitignore
git commit -m "Track data and models with DVC"
```

### Configure Remote Storage

DVC needs a remote storage location (like S3, Google Drive, or local directory):

```bash
# Option 1: Local backup directory
dvc remote add -d myremote /path/to/backup/folder

# Option 2: AWS S3
dvc remote add -d myremote s3://mybucket/dvc-storage

# Option 3: Google Drive
dvc remote add -d myremote gdrive://1dyPnS7_8...
```

### Push/Pull Data

```bash
# Push tracked data to remote
dvc push

# Pull data from remote (when cloning repo)
dvc pull

# Pull specific file
dvc pull data/sentiment140_sampled_200k.csv.dvc
```

### Check Status

```bash
# Check which files are tracked
dvc status

# List all tracked files
dvc list . -R
```

## Workflow Example

### Initial Setup (First Time)
```bash
# 1. Track large files
dvc add data/training.1600000.processed.noemoticon.csv
dvc add models/bertweet_sentiment_finetuned

# 2. Commit DVC files to Git
git add data/*.dvc models/*.dvc
git commit -m "Track large files with DVC"

# 3. Push data to remote storage
dvc push
```

### Collaborator Setup (Cloning)
```bash
# 1. Clone the repository
git clone https://github.com/sean-mas/XAI-Project.git
cd XAI-Project

# 2. Install dependencies including DVC
pip install -r requirements.txt

# 3. Pull tracked data
dvc pull
```

### Updating Data/Models
```bash
# 1. Make changes to tracked files
# (e.g., retrain model, add new data)

# 2. Update DVC tracking
dvc add models/bertweet_sentiment_finetuned

# 3. Commit changes
git add models/bertweet_sentiment_finetuned.dvc
git commit -m "Update fine-tuned model - v2"

# 4. Push new data
dvc push
```

## Benefits

✅ **Version Control for Data**: Track dataset versions alongside code  
✅ **Reproducibility**: Others can pull exact datasets used in experiments  
✅ **Collaboration**: Team members share large files without bloating Git repo  
✅ **Storage Efficiency**: Only stores changed files, not full copies  

## Current Configuration

- **Git Tracked**: `.dvc/` directory (DVC config)
- **Git Ignored**: Actual data files in `data/` and `models/`
- **DVC Tracked**: Large files referenced in `.dvc` files
- **Remote**: Not yet configured (see "Configure Remote Storage" above)

## Next Steps

1. ✅ DVC initialized
2. ⏳ Configure remote storage (when ready to share)
3. ⏳ Track data files (after running Notebook 3)
4. ⏳ Track models (after running Notebook 4)
5. ⏳ Push to remote (for backup/sharing)

## Documentation

- [DVC User Guide](https://dvc.org/doc/user-guide)
- [DVC with Git](https://dvc.org/doc/use-cases/versioning-data-and-model-files)
- [Remote Storage](https://dvc.org/doc/command-reference/remote)
