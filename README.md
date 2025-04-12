# 🧬 PCA Reference File Setup & Hail Environment on MacBook (ARM64)

This guide helps you set up Hail on a MacBook with ARM64 and do ancestry estimation using vcf file from nf-core pipeline Sarek, by using pre-calculated pcs so that you do not need much computation power or time. Note that there is caveat to this method, please refer to https://gnomad.broadinstitute.org/news/2021-09-using-the-gnomad-ancestry-principal-components-analysis-loadings-and-random-forest-classifier-on-your-dataset/

---

## 📥 Downloading PCA Reference File from Google Cloud

### 1. Install Google Cloud SDK

```bash
curl https://sdk.cloud.google.com | bash
```

- Follow the instructions and update your `~/.bashrc` or `~/.bash_profile` as prompted.

### 2. Download PCA Reference Data

```bash
gsutil -m cp -r -n gs://gcp-public-data--gnomad/release/4.0/pca/gnomad.v4.0.pca_loadings.ht ./
```

---

## 🍎 Setting Up Hail on MacBook (Apple Silicon)

### 1. Install Homebrew (if not already installed)

Visit [https://brew.sh](https://brew.sh) and follow installation instructions.

### 2. Install Required Dependencies

```bash
brew install conda gcc openblas pkg-config postgresql
```

### 3. Configure Environment Variables

Add the following to your `~/.bashrc` or `~/.bash_profile`:

```bash
export LDFLAGS="-L$(brew --prefix openblas)/lib"
export CPPFLAGS="-I$(brew --prefix openblas)/include"
export PKG_CONFIG_PATH="$(brew --prefix openblas)/lib/pkgconfig"
export BLAS="$(brew --prefix openblas)/lib/libblas.dylib"
export LAPACK="$(brew --prefix openblas)/lib/liblapack.dylib"
```

Then apply the changes:

```bash
source ~/.bashrc  # or source ~/.bash_profile
```

---

## 📦 Install Python Dependencies

Install required Python packages with `pip`:

```bash
pip install scipy notebook ipykernel hail psycopg2-binary gnomad gcsfs google-cloud-storage
```

---

## 🧬 Clone gnomAD QC Repository

```bash
git clone https://github.com/broadinstitute/gnomad_qc.git
pip install gnomad_qc
```

---

## ☁️ Install Google Cloud SDK via Conda for later use

```bash
conda install -c conda-forge google-cloud-sdk
```

---

## ✅ Done!

You're now ready to run .ipynb for ancestry calculation.

---

Feel free to contribute or raise issues if you encounter problems!
