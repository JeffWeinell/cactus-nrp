# Running Progressive Cactus step-by-step using NRP cluster and S3 storage

These steps may be useful for AMNH Herpetology lab members that have access to NRP resources.

#### What you will need at start
- NRP cluster credentials
- NRP S3 credentials
- assembled genomes (*.fa.gz files)
- 'rclone', to create/configure/organize your S3 bucket environment. I installed this locally and in a conda environment on mendel
- 'kubectl', to manage cluster jobs. I installed this locally.

#### Organize S3 bucket
For the following code, replace 'mybucket' with the name of your storage bucket.

```
# Create a directory to hold your genome assemblies:
rclone mkdir mybucket:genomes

# Create a directory to hold 'preprocessed' genome assemblies (outputs of cactus-preprocess):
rclone mkdir mybucket:genomes-preprocessed

# Transfer genomes to mybucket:genomes
rclone copy </src/path/to/genome1.fa.gz> mybucket:genomes
rclone copy </src/path/to/genome2.fa.gz> mybucket:genomes
rclone copy </src/path/to/genomeN.fa.gz> mybucket:genomes
```

#### Create some kubernetes secrets
- Download these files from this repository: apps.sh, rclone.config, cactus-prepare, cactus-preprocess-genome, and cactus-blast-align-hal2fasta
- Add your NRP S3 credentials to the file rclone.config
- Create a kubernetes secret from each file
```
kubectl create secret generic apps --from-file=/path/to/apps.sh
kubectl create secret generic rclone --from-file=/path/to/rclone.config
kubectl create secret generic cactus-prepare --from-file=/path/to/cactus-prepare
kubectl create secret generic cactus-preprocess-genome --from-file=/path/to/cactus-preprocess-genome
kubectl create secret generic cactus-blast-align-hal2fasta --from-file=/path/to/cactus-blast-align-hal2fasta
```

#### 






