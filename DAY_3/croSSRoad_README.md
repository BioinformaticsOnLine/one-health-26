# croSSRoad

croSSRoad is available in both **GUI** and **CLI** formats.

## 🔗 GUI and CLI Links

- **GUI:** https://crossroad.bioinformaticsonline.com/analysis  
- **CLI (GitHub):** https://github.com/BioinformaticsOnLine/croSSRoad  

---

## ⚙️ Installation Steps

```bash
conda create -n crossroad -y
conda activate crossroad
conda install conda-forge::mamba -y
mamba install crossroad -c jitendralab -c bioconda -c conda-forge --channel-priority flexible -y
```

**Check version:**
```bash
crossroad -v
```
> Expected version: `0.3.6`

---

## 📂 Fetch Data

```bash
cp -r /home/workshop/4b_data/test_data/ .
```

---

## 🚀 Usage

### 🔹 First Mode

```bash
crossroad -fa 1.fa -o out1
```

```bash
crossroad -fa 1.fa -l 170000 -L 220000 -o out1_filter
```

---

### 🔹 Second and Third Mode

```bash
crossroad -fa 1.fa -c 3.tsv -b 2.bed -p
```

```bash
crossroad -i input_directory -p \
  --mono 12 --di 4 --tri 3 --tetra 3 --penta 3 --hexa 2 \
  -l 170000 -L 220000 \
  -ref NC_063383.1 \
  -o output_directory
```

---

## ✅ Notes

- Ensure Conda is properly installed before starting.
- Use `mamba` for faster dependency resolution.
- Adjust parameters based on your dataset and analysis requirements.

---
