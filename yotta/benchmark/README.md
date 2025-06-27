# 🧠 Wan2.1 T2V (Text-to-Video) - RTX 5090 vs H100

This repository outlines the steps to set up and run the [Wan2.1](https://github.com/Wan-Video/Wan2.1) Text-to-Video model.

---

## 📦 Environment Setup

```bash
# Create and activate a Python virtual environment
python3 -m venv venv
source venv/bin/activate
```

---

## 🔧 Install PyTorch (CUDA 12.8) on RTX 5090, Skip this for H100

```bash
pip install torch==2.7.0+cu128 torchvision torchaudio \
  --index-url https://download.pytorch.org/whl/cu128
```

---

## ⚡ Install FlashAttention on RTX 5090, Skip this for H100

```bash
# Download the prebuilt FlashAttention wheel (only for RTX 5090)
wget https://github.com/Zarrac/flashattention-blackwell-wheels-whl-ONLY-5090-5080-5070-5060-flash-attention-/releases/download/FlashAttention/flash_attn-2.7.4.post1-rtx5090-torch2.7.0cu128cxx11abiTRUE-cp312-linux_x86_64.whl

# Rename for clarity/compatibility
mv flash_attn-2.7.4.post1-rtx5090-*.whl \
   flash_attn-2.7.4.post1-0rtx5090torch270cu128cxx11abiTRUE-cp312-cp312-linux_x86_64.whl

# Install it
pip install flash_attn-2.7.4.post1-0rtx5090torch270cu128cxx11abiTRUE-cp312-cp312-linux_x86_64.whl
```

---

## 🚀 Clone & Install Wan2.1

```bash
git clone https://github.com/Wan-Video/Wan2.1.git
cd Wan2.1

pip install -r requirements.txt
pip install "huggingface_hub[cli]"
```

---

## 📥 Download Model Weights

```bash
huggingface-cli download Wan-AI/Wan2.1-T2V-1.3B --local-dir ./Wan2.1-T2V-1.3B
```

---

## 🧪 Run Inference


```bash
python generate.py \
  --task t2v-1.3B \
  --size 480*832 \
  --ckpt_dir ./Wan2.1-T2V-1.3B \
  --prompt "Two anthropomorphic cats in comfy boxing gear and bright gloves fight intensely on a spotlighted stage."
```


---

## Example Output
```bash
[2025-06-27 04:02:34,158] INFO: Creating WanT2V pipeline.
[2025-06-27 04:03:20,511] INFO: loading ./Wan2.1-T2V-1.3B/models_t5_umt5-xxl-enc-bf16.pth
[2025-06-27 04:03:27,097] INFO: loading ./Wan2.1-T2V-1.3B/Wan2.1_VAE.pth
[2025-06-27 04:03:27,442] INFO: Creating WanModel from ./Wan2.1-T2V-1.3B
[2025-06-27 04:03:28,721] INFO: Generating video ...
100%|████████████████████████████████████████████████████████████████████████| 50/50 [02:58<00:00,  3.57s/it]
[2025-06-27 04:06:44,223] INFO: Saving generated video to t2v-1.3B_480*832_1_1_Two_anthropomorphic_cats_in_comfy_boxing_gear_and__20250627_040644.mp4
[2025-06-27 04:06:45,721] INFO: Finished.
```

---
## H100 vs RTX 5090 

| Metric           | RTX 5090     | H100         |
|------------------|--------------|--------------|
| Inference Time   | ~3m 17s      | ~1m 31s      |
| Avg Step Time    | ~3.57 s/step | ~1.83 s/step |

