# 🧠 Wan2.1 T2V (Text-to-Video) - RTX 5090 Setup

This repository outlines the steps to set up and run the [Wan2.1](https://github.com/Wan-Video/Wan2.1) Text-to-Video model, optimized for NVIDIA RTX 5090 using PyTorch 2.7.0 (CUDA 12.8) and a custom FlashAttention wheel.

---

## 📦 Environment Setup

```bash
# Create and activate a Python virtual environment
python3 -m venv venv
source venv/bin/activate
```

---

## 🔧 Install PyTorch (CUDA 12.8)

```bash
pip install torch==2.7.0+cu128 torchvision torchaudio \
  --index-url https://download.pytorch.org/whl/cu128
```

---

## ⚡ Install FlashAttention (RTX 5090 Wheel)

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



