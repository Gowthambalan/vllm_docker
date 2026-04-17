# 🚀 vLLM Small Model Deployment (Docker)

This project provides a simple **Docker Compose setup** to run a lightweight LLM using **vLLM OpenAI-compatible API**.

---

## 📌 Overview

* Uses **vLLM** for high-performance inference
* Runs **Qwen2.5-0.5B-Instruct** (lightweight & fast)
* GPU-enabled via NVIDIA
* Exposes OpenAI-compatible API on **port 8000**

---

## 🧰 Tech Stack

* Docker & Docker Compose
* vLLM (OpenAI API compatible server)
* NVIDIA GPU (CUDA required)
* Hugging Face Hub

---

## ⚙️ Prerequisites

Make sure you have:

* Docker installed
* NVIDIA GPU + drivers
* NVIDIA Container Toolkit installed
  👉 https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html
* Hugging Face token

---

## 🔑 Setup

### 1. Clone Repository

```bash
git clone https://github.com/your-username/vllm-small-deploy.git
cd vllm-small-deploy
```

### 2. Set Hugging Face Token

```bash
export HF_TOKEN=your_huggingface_token
```

---

## ▶️ Run the Service

```bash
docker-compose up -d
```

---

## 🌐 API Endpoint

Once running:

```
http://localhost:8000
```

OpenAI-compatible endpoints:

* `POST /v1/completions`
* `POST /v1/chat/completions`

---

## 🧪 Example Request

```bash
curl http://localhost:8000/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "Qwen/Qwen2.5-0.5B-Instruct",
    "messages": [
      {"role": "user", "content": "Hello, how are you?"}
    ]
  }'
```

---

## ⚙️ Configuration

Key parameters in `docker-compose.yml`:

| Parameter                  | Description                            |
| -------------------------- | -------------------------------------- |
| `--model`                  | Model name from Hugging Face           |
| `--dtype`                  | Precision (float16 for GPU efficiency) |
| `--max-model-len`          | Context length                         |
| `--gpu-memory-utilization` | GPU memory usage limit                 |
| `--max-num-seqs`           | Parallel requests                      |
| `--swap-space`             | CPU swap for overflow                  |

---

## 📁 Volume Mapping

```bash
~/.cache/huggingface:/root/.cache/huggingface
```

* Caches model locally
* Avoids repeated downloads

---

## 🔄 Restart Policy

```yaml
restart: unless-stopped
```

Ensures container auto-restarts unless manually stopped.

---

## ⚡ Performance Tips

* Increase `gpu-memory-utilization` if GPU has more VRAM
* Increase `max-num-seqs` for higher concurrency
* Use larger models if GPU allows

---

## 🐞 Troubleshooting

### GPU Not Detected

```bash
docker run --gpus all nvidia/cuda:12.0-base nvidia-smi
```

### Model Download Issues

* Verify `HF_TOKEN`
* Ensure internet access

---

## 📌 Notes

* This setup is optimized for **low-resource environments**
* Suitable for:

  * Prototyping
  * API testing
  * Lightweight AI apps

---

## 📜 License

MIT License

---

## 🙌 Contributing

Feel free to open issues or submit PRs!

---
