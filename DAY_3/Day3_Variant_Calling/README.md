# 🧬 SNP Calling Pipeline using BCFtools

This pipeline describes how to perform read alignment and variant (SNP) calling from raw FASTQ files using bwa, samtools, and bcftools.

## 📦 Requirements

bwa  
samtools  
bcftools  
tabix (optional)

## 📁 Input Data

- Reference genome: ref.fa  
- Paired-end reads: sample_R1.fastq.gz, sample_R2.fastq.gz  

## 🧭 Workflow Overview

1. Index reference genome  
2. Align reads to reference  
3. Convert SAM → BAM, sort, index  
4. Generate pileup  
5. Call variants  
6. Filter SNPs  

## 🔧 Step-by-Step Pipeline

### 1️⃣ Index the Reference Genome

bwa index ref.fa  
samtools faidx ref.fa  

### 2️⃣ Align Reads with BWA-MEM

bwa mem -t 8 ref.fa sample_R1.fastq.gz sample_R2.fastq.gz > sample.sam  

### 3️⃣ Convert SAM to BAM, Sort and Index

samtools view -bS sample.sam > sample.bam  
samtools sort -@ 8 -o sample.sorted.bam sample.bam  
samtools index sample.sorted.bam  

### 4️⃣ Generate Pileup and Call Variants

bcftools mpileup -Ou -f ref.fa sample.sorted.bam | bcftools call -mv -Oz -o sample.vcf.gz  

### 5️⃣ Index the VCF File

bcftools index sample.vcf.gz  

### 6️⃣ Filter SNPs

bcftools view -v snps sample.vcf.gz -Oz -o sample.snps.vcf.gz  
bcftools index sample.snps.vcf.gz  

bcftools filter -e 'QUAL<30 || DP<10' sample.snps.vcf.gz -Oz -o sample.filtered.vcf.gz  
bcftools index sample.filtered.vcf.gz  

## 📊 Optional: Multi-sample Variant Calling

bcftools mpileup -Ou -f ref.fa *.sorted.bam | bcftools call -mv -Oz -o cohort.vcf.gz  

## 🧪 Output Files

- sample.sorted.bam  
- sample.vcf.gz  
- sample.snps.vcf.gz  
- sample.filtered.vcf.gz  

## 🧹 Cleanup (Optional)

rm *.bam.bai  

## 📌 Notes

- Suitable for haploid and diploid organisms  
- Adjust filtering thresholds as needed  
