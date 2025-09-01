# NCN On-Road Quietway Assessment

This project assesses **on-road sections** of the National Cycle Network (NCN) to determine whether they meet the Quietway standard, using Sustrans’ internal matrix:
- Traffic speed and volume data from *Agilysis*
- NCN On Road Section data from *Sustrans*

The repository contains a single Jupyter Notebook that processes the input data, applies a scoring matrix, and outputs GIS-ready layers and summary tables for further analysis or mapping.

---

- **`Quietway_Assessment.ipynb`** — Main analysis workflow

---

## 🔧 Parameters Can Be Changed

Variables in the notebook to fit local policy, context, or data availability.

### 📏 Buffers
- `buffer = 10` — Buffer size (in meters) used to overlay Agilysis data.
- `percent_in_buffer = 0.9` — Minimum proportion of the feature within the buffer to be included.

### 🚦 Speed & Volume Fields Used
- **`85th %ile Speed - All Day`** — 85th percentile speed (`p85` speed).
- **`Modelled AADT`** — Annual Average Daily Traffic volume.

### 📝 Scoring Matrix
Adjust the scoring matrices below to adapt to local policy.
**Matrix for segments *outside* buffer (`matrix_outwith`):**
```python
matrix_outwith = {
    "<500": {"<20": "Definitely Quietway", "20-30": "Definitely Quietway", "30-40": "Likely Quietway", ">40": "Make Quietway"},
    "500-1000": {"<20": "Definitely Quietway", "20-30": "Likely Quietway", "30-40": "Likely Quietway", ">40": "Make Quietway"},
    "1000-2000": {"<20": "Make Quietway", "20-30": "Make Quietway", "30-40": "Make Quietway", ">40": "Make Quietway"},
    "2000-4000": {"<20": "Make Quietway", "20-30": "Make Quietway", "30-40": "Make Quietway", ">40": "Make Traffic Free"},
    "4000-10000": {"<20": "Make Traffic Free", "20-30": "Make Traffic Free", "30-40": "Make Traffic Free", ">40": "Make Traffic Free"},
    ">10000": {"<20": "Make Traffic Free", "20-30": "Make Traffic Free", "30-40": "Make Traffic Free", ">40": "Make Traffic Free"}
}
