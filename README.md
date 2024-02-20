# Enterprise AI Inference Gateway & Multi-Backend Model Server

[![CI](https://github.com/yousefkhaled2005/enterprise-ai-inference-engine/actions/workflows/ci.yml/badge.svg)](https://github.com/yousefkhaled2005/enterprise-ai-inference-engine)
[![Languages](https://img.shields.io/badge/Languages-Go%20%7C%20C%2B%2B%20%7C%20Python%20%7C%20C%20%7C%20CUDA%20%7C%20Rust-blueviolet.svg)](api/)
[![API](https://img.shields.io/badge/API-OpenAI%20Compatible%20REST%20%7C%20gRPC-teal.svg)](api/)
[![Multi-Backend](https://img.shields.io/badge/Backends-llama.cpp%20%7C%20Whisper%20%7C%20StableDiffusion%20%7C%20vLLM-orange.svg)](core/)
[![License](https://img.shields.io/badge/License-MIT-purple.svg)](LICENSE)

A high-performance, polyglot AI inference gateway and multi-modal model server engineered for mission-critical enterprise production. Serves Large Language Models (LLMs), Automatic Speech Recognition (ASR), Computer Vision, and Image Generation across commodity CPUs, NVIDIA GPUs, AMD ROCm, and Apple Silicon.

Architected and maintained by **Yousef Khaled** (Senior AI Systems Architect). Features a high-concurrency **Go** HTTP/gRPC gateway, hardware-accelerated **C++** SIMD execution runtimes (AVX-512, CUDA, TensorRT), **Python** PyTorch transformer bridges, and complete drop-in OpenAI API compatibility.

---

## 🏛 Multi-Language System Architecture

```
                                [Client Applications]
                     (OpenAI SDK, LangChain, LlamaIndex, cURL)
                                         │
                                         ▼
                     +─────────────────────────────────────────+
                     |         Go Concurrency Gateway          |
                     |  - High-Throughput HTTP / gRPC Router   |
                     |  - Token Streaming & SSE Dispatcher     |
                     |  - Model Gallery & Hot-Swapping Cache   |
                     +─────────────────────────────────────────+
                                         │
                 ┌───────────────────────┼───────────────────────┐
                 ▼                       ▼                       ▼
   +──────────────────────────+ +─────────────────────────+ +─────────────────────────+
   |   C++ SIMD Model Core    | |  Python PyTorch Bridge  | |   Audio / Vision C++    |
   | - llama.cpp Runtime      | | - Hugging Face Hub      | | - whisper.cpp (ASR)     |
   | - CUDA / ROCm / Vulkan   | | - Transformers / Diff   | | - LLaVA / CLIP (Vision) |
   | - Zero Memory Copy       | | - gRPC IPC Worker Pool  | | - Stable Diffusion      |
   +──────────────────────────+ +─────────────────────────+ +─────────────────────────+
                 └───────────────────────┬───────────────────────┘
                                         ▼
                     +─────────────────────────────────────────+
                     |    Unified Enterprise Hardware Layer    |
                     |     (NVIDIA A100/H100 / Apple / CPU)    |
                     +─────────────────────────────────────────+
```

---

## ⚡ Polyglot Engineering Stack

| Language | Volume | Component & Responsibility |
| :--- | :--- | :--- |
| 🐹 **Go** | ~19.2 MB | Main HTTP REST router, SSE streaming worker pool, gRPC gateway, dynamic process supervisor. |
| ⚙️ **C++ / C** | ~7.7 MB | High-performance inference engines: `llama.cpp`, `whisper.cpp`, hardware quantization, CUDA kernels. |
| 🐍 **Python** | ~1.2 MB | PyTorch model adapters, Hugging Face transformers worker bridge, tokenization pipelines. |
| 📘 **TypeScript / JS**| ~4.2 MB | Integrated web management portal and model gallery UI. |
| 🐚 **Shell / Make** | ~800 KB | Cross-platform build automation, multi-target container compilation (Linux, macOS, Windows). |

---

## 🚀 Unified OpenAI-Compatible API

```bash
# Chat Completion Streaming
curl http://localhost:8080/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "arabic-llm",
    "messages": [{"role": "user", "content": "اشرح لي معمارية الأنظمة الموزعة بالتفصيل"}],
    "stream": true
  }'
```

```bash
# Audio Transcription (Whisper)
curl http://localhost:8080/v1/audio/transcriptions \
  -H "Content-Type: multipart/form-data" \
  -F file="@call_audio.wav" \
  -F model="whisper-1"
```

---

## 📜 License
Distributed under the MIT License. See [LICENSE](LICENSE) for details.
