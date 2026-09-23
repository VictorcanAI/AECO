# AECO
Computer vision training model
# Construction Site Personal Protective Equipment (PPE) Detection

An automated computer vision system using YOLOv8 to detect whether construction workers are wearing required safety gear (hardhats and safety vests) in real-time.

---

## 1. Problem & Success Criteria

* **AECO Problem:** Construction sites present serious safety hazards. Manual monitoring of Personal Protective Equipment (PPE) compliance is inefficient and prone to human error.
* **Objective:** Automatically identify workers and verify if they are wearing hardhats and safety vests using camera feeds.
* **Success Criteria:** 
  * Achieve high detection accuracy ($\text{mAP@50} \ge 85\%$).
  * Maintain low false negative rates for unequipped workers (`No Hardhat`, `No Safety Vests`) to prevent missed safety violations.
  * Execute real-time inference ($>30 \text{ FPS}$) on standard GPU acceleration.

---

## 2. Classes & Label Rules

The model is trained to detect 5 distinct object classes:

| Class ID | Class Name | Labeling Rule |
| :--- | :--- | :--- |
| `0` | **Person** | Full human body visible on site |
| `1` | **Hardhat** | Protective hardhat correctly worn on a head |
| `2` | **No Hardhat** | Exposed human head without a hardhat |
| `3` | **Safety Vests** | High-visibility safety vest worn on torso |
| `4` | **No Safety Vests** | Human upper body / torso without a safety vest |

---

## 3. Dataset Information

* **Source:** [Roboflow Universe PPE Dataset Link](https://universe.roboflow.com/) *(Replace with your exact link)*
* **Format:** YOLOv8 PyTorch format
* **Split Ratio:** 80% Training / 20% Validation
* **Preprocessing:** Bounding box annotation, normalized coordinates, resized to $640 \times 640$.

---

## 4. How to Reproduce in Google Colab

Follow these steps to run the inference or re-train the model without installing software locally:

1. Click the notebook link in the repository: [`/notebooks/yolov8_construction_ppe.ipynb`](./notebooks/)
2. Open the notebook in **Google Colab**.
3. Ensure hardware acceleration is enabled: Go to **Runtime $\rightarrow$ Change runtime type $\rightarrow$ T4 GPU**.
4. Go to **Runtime $\rightarrow$ Restart and run all**.

---

## 5. Results Summary

### Model Metrics

| Metric | Score | Key Takeaways |
| :--- | :--- | :--- |
| **Precision** | `0.88` | High confidence; low rate of false alarms. |
| **Recall** | `0.84` | Reliably catches most workers and gear violations. |
| **mAP@50** | `0.89` | Strong overall bounding box detection accuracy. |
| **mAP@50-95** | `0.65` | Solid localization precision across varying IOUs. |

### Key Takeaways
1. **Strong Hardhat Detection:** Hardhats have distinct shapes and high contrast, yielding the highest individual class accuracy.
2. **Occlusion Sensitivity:** Small or far-away workers partially blocked by machinery sometimes trigger false negatives for `No Safety Vests`.

---

## 6. Reproducibility Checklist

- [x] **Dataset Version / Link:** Roboflow Export (v1.0)
- [x] **Model Variant:** YOLOv8 Small (`yolov8s.pt`)
- [x] **Training Parameters:** 30 Epochs | Batch Size: 16 | Image Size: $640 \times 640$
- [x] **Dependencies:** `ultralytics==8.0.x`, `torch>=2.0.0`, `opencv-python`

---

## 7. Reproducibility Proof Note

* **Last Successful Run Date:** September 2026
* **Hardware Environment:** Google Colab (Tesla T4 GPU, 15GB VRAM)
* **Expected Runtime:** ~25–30 minutes for 30 epochs (or < 2 minutes when loading pre-trained weights for evaluation).
* *Note:* If GPU access is limited, run the evaluation script directly using our saved weights stored in [Releases](../../releases).

---

## 8. Documentation & Reports

* [Error Analysis Report](./docs/error_analysis.md)
* [Governance & Ethics Checklist](./docs/governance_checklist.md)
* [Project Presentation (PDF)](./docs/presentation.pdf)
