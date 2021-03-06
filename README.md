# nextflow-aws-batch-issue-1024


## Data sets
 - Large: s3://nextflow-datasets/52-samples/fastqs
 - Small: s3://nextflow-datasets/2-samples/fastqs

## Running the workflow
Two requirements

 - Substitute <S3 FASTQ FOLDER> for one of the base S3 folders nextflow-datasets/52-samples or nextflow-datasets/2-samples. These are publically readable.
 - Substitute <S3 BUCKET WRITABLE FOLDER> for a S3 bucket/folder you have write permissions for.
 - Substitute <AWS BATCH QUEUE> for an AWS Batch queue you have permissions for. 

```
nextflow run assembly.nf -ansi -profile aws_batch -resume \
-work-dir s3://<S3 BUCKET WRITABLE FOLDER>/workdir \
--input_dir s3://<S3 FASTQ FOLDER>/fastqs \
--output_dir s3://<S3 BUCKET WRITABLE FOLDER>/output \
--fastq_pattern '*_{1,2}.fastq.gz' \
--adapter_file adapters.fas  \
--depth_cutoff 100 \
--qc_conditions qc_conditions.yml \
--aws_batch_queue <AWS BATCH QUEUE>
```