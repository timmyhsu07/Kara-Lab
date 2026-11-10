# Kara-Lab

Studying the Neurobiology of Neurodegenerative Disease

The mission of the lab is to follow a network-based approach to understand the pathogenesis of neurodegenerative diseases, with the ultimate aim being to utilize this strategy to develop combination treatments. This strategy distinguishes our lab from a decades-long tradition in the field of zeroing in on specific genes and focusing on the development of monotherapies for the treatment of neurodegenerative diseases.

Simultaneously, the lab aspires to remain at the cutting edge in terms of cellular and molecular biology techniques and to advance the neurodegeneration field by developing innovative tools and technologies that we will share with the research community.

## Repository guide

| Folder | Contents |
|---|---|
| `analyses_of_alpha-synuclein_biomolecular_condensates/` | Current analyses: C12 and oleic acid pulse-chase, FRAP, TMRM z-stacks, linoleic acid, mitophagy, tiles, and ML segmentation (U-Net, U-Net++, micro-SAM) |
| `synuclein_inclusion_biogenesis_2024/` | Code for the 2024 inclusion biogenesis work: image analysis notebooks, ML segmentation, and WGCNA gene-list analysis. See `image_analysis/Introduction to Code Files.txt` |
| `image_analysis_methods_2025/` | Methods notebooks: reading image files, parsing CZI metadata, preprocessing, measurements, and figure code, plus the inclusion annotation dataset |
| `lipid droplet homeostasis/` | Placeholder |
| `document_word_checker/` | Utility that processes a Word document (see its `readme`) |

Most analyses are standalone Jupyter notebooks. Each one reads `.czi` images from a folder you set near the top of the notebook and writes CSVs and QC figures next to it.

## Setup

Python 3.12 was used for most notebooks.

```bash
git clone https://github.com/timmyhsu07/Kara-Lab.git
cd Kara-Lab
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
```

### Image analysis notebooks (most of the repo)

```bash
pip install "cellpose<4" czifile aicspylibczi tifffile numpy pandas scipy scikit-image \
    matplotlib opencv-python imageio pillow openpyxl tqdm jupyter
```

Cellpose must be below version 4. These notebooks use `models.Cellpose(model_type=...)`, which was removed in Cellpose 4.

Before running a notebook:

1. Set the image folder path(s) in the first parameters cell.
2. Set `USE_GPU = False` if you have no CUDA GPU.
3. Run top to bottom and check the QC figures.

### ML segmentation (`machine_learning/` folders)

- **Prediction notebooks** need `torch`, `torchvision`, and `huggingface_hub`. Trained weights are downloaded from the Hugging Face repo `sunny17347/machine_learning_models` (for example `U_NET_7_8_2025.pth`, `unetpp_trained_7_8_2025.pth`, `SAM_finetuned.pt`).

  ```bash
  pip install torch torchvision huggingface_hub
  ```

- **micro-SAM** (`micro_sam`, `torch_em`): the notebook installs it from conda-forge. Either of these works locally:

  ```bash
  conda install -c conda-forge micro_sam
  # or
  pip install micro_sam
  ```

- **Training notebooks** (`training_scripts/`) were written for Google Colab and read data from a mounted Google Drive (`/content/drive`). Run them in Colab, or change the Drive paths to local ones.

### Other folders

- `synuclein_inclusion_biogenesis_2024/WGCNA/`: `pip install pandas scipy requests strsimpy openpyxl`
- `image_analysis_methods_2025/reading_image_files/`: also needs `readlif` and `nd2` for Leica and Nikon files.
- `document_word_checker/`: `pip install Spire.Doc`
- `C12_pulse_chase/C12_pulse_chase.ipynb` imports `SegmentClassifyPipeline` from an `inclusion_pipeline` module that is not in this repo. You need that module on your path to run this notebook.
