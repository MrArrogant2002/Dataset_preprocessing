# Processed Medical Image Datasets for BoundMamba

This repository contains **five preprocessed 2D medical image segmentation datasets** formatted uniformly for training deep learning models, especially Mamba-based architectures like BoundMamba. All datasets have been resized to **256×256 pixels**, split into **train/val/test** folders (or using the official splits where available), and saved as PNG files for fast loading and compatibility.

---

## 📁 Folder Structure

Each dataset is organized as:

```
dataset_name/
  train/
    images/    (RGB PNG files)
    masks/     (grayscale PNG files, same filename)
  val/
    images/
    masks/
  test/
    images/
    masks/
```

- **Images** are 3-channel RGB PNG.
- **Masks** are single-channel grayscale PNG. For binary segmentation tasks, mask values are **0 (background) and 255 (foreground)**. For multi‑class segmentation (Synapse), mask values are **0 (background), 1, 2, …, 8** (the 8 organs).

---

## 📊 Dataset Details

| Dataset | Original Source | Original Modality | Original Size | Preprocessing |
|---------|-----------------|-------------------|---------------|----------------|
| **ISIC2018** | [ISIC 2018 Challenge](https://challenge.isic-archive.com/landing/2018/) | Dermoscopy images | Variable (mostly ~600×450) | Used official train/val/test splits; resized to 256×256; masks binarized (0/255). |
| **ISIC2017** | [ISIC 2017 Challenge](https://challenge.isic-archive.com/landing/2017/) | Dermoscopy images | 32×32 (downloaded from a Kaggle version) | Merged `trainx`/`trainy` to create train/val/test (80/10/10); resized to 256×256; masks binarized. |
| **PH2** | [PH² dataset](https://www.fc.up.pt/addi/ph2%20database.html) | Dermoscopy images | 768×560 | Random split 80/10/10; resized to 256×256; masks binarized. |
| **CVC-ClinicDB** | [CVC-ClinicDB](https://www.kaggle.com/datasets/balraj98/cvcclinicdb) | Endoscopic polyp images | 384×288 | Random split 80/10/10; resized to 256×256; masks binarized. |
| **Synapse** | [MICCAI 2015 Multi-Atlas Abdomen Challenge](https://www.synapse.org/#!Synapse:syn3193805/wiki/217752) | Abdominal CT volumes (3D) | 512×512×(~80–200) | Converted 3D volumes to axial 2D slices; applied standard CT windowing (-125 to 275 HU); resized to 256×256; saved only slices containing at least one organ (to reduce class imbalance). Patient‑wise split: first 18 for training, next 12 for testing; training further split 90/10 into train/val. Mask labels: 0 = background, 1 = spleen, 2 = right kidney, 3 = left kidney, 4 = gallbladder, 5 = liver, 6 = stomach, 7 = aorta, 8 = pancreas. |

---

## 🔧 Preprocessing Steps (Applied to All)

1. **Resizing**: All images and masks are resized to **256×256** using bilinear interpolation for images and nearest‑neighbor for masks.
2. **Normalization**: Images are not globally normalized; they are stored as original RGB values (0–255). For Synapse, CT values are clipped to the soft‑tissue window (-125 to 275 HU) and scaled to 0–255.
3. **Splits**: Train/val/test splits are either the official ones (ISIC2018, Synapse) or a consistent 80/10/10 random split with fixed seed (42) for reproducibility.
4. **File naming**: Filenames are derived from the original base names; for Synapse, slices are numbered sequentially per patient.



## 📄 Citation

If you use this preprocessed data in your research, please cite the original datasets as well as this preprocessing effort:

- **ISIC 2018/2017**: The International Skin Imaging Collaboration (ISIC) Archive.  
- **PH2**: Mendonça, T., et al. (2013). PH2 – A dermoscopic image database for research and benchmarking.  
- **CVC-ClinicDB**: Bernal, J., et al. (2015). WM-DOVA maps for accurate polyp highlighting in colonoscopy.  
- **Synapse**: Landman, B., et al. (2015). MICCAI 2015 Multi-Atlas Abdomen Labeling Challenge.

*Preprocessing scripts available at [GitHub repo] (optional).*

---

## 📦 Download

The processed dataset is available on Kaggle: **https://www.kaggle.com/datasets/eswarbalu/processed-dataset**.
---
