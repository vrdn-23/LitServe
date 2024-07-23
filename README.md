<div align="center">

<img alt="Lightning" src="https://pl-bolts-doc-images.s3.us-east-2.amazonaws.com/app-2/ls_banner2.png" width="800px" style="max-width: 100%;">

<br/>
<br/>

**High-throughput serving engine for AI models.    
Friendly interface. Enterprise scale.**

<pre>
✅ Batching       ✅ Streaming          ✅ Auto-GPU, multi-GPU   
✅ Multi-modal    ✅ PyTorch/JAX/TF     ✅ Full control          
✅ Auth           ✅ Built on Fast API  ✅ Custom specs (Open AI)
</pre>



---

[![license](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://github.com/Lightning-AI/litserve/blob/main/LICENSE)
![PyPI - Python Version](https://img.shields.io/pypi/pyversions/litserve)
![cpu-tests](https://github.com/Lightning-AI/litserve/actions/workflows/ci-testing.yml/badge.svg) [![Discord](https://img.shields.io/discord/1077906959069626439?label=Get%20Help%20on%20Discord)](https://discord.gg/VptPCZkGNa)

<p align="center">
  <a href="https://lightning.ai/">Lightning AI</a> •
  <a href="#quick-start">Quick start</a> •
  <a href="#featured-examples">Examples</a> •
  <a href="#deployment-options">Deploy</a> •
  <a href="#features">Features</a> •
  <a href="#performance">Benchmarks</a> •
  <a href="https://lightning.ai/docs/litserve">Docs</a>
</p>

<p align="center">

&nbsp;
  
<a target="_blank" href="https://lightning.ai/docs/litserve/home">
  <img src="https://pl-bolts-doc-images.s3.us-east-2.amazonaws.com/app-2/get-started-badge.svg" height="36px" alt="Get started"/>
</a>

</p>

</div>

&nbsp;

# Deploy AI models Lightning fast ⚡

<table>
  <tr>
    <td>
LitServe is a <strong>high-throughput serving engine</strong> built on FastAPI, designed to deploy AI models at scale with features like batching, streaming, and autoscaling across CPUs and GPUs.
      <br><br>
LitServe provides a ready-to-use server with AI-specific techniques, eliminating the need to build a new FastAPI server for each model.
    </td>
    <td>
      <a href="https://github.com/Lightning-AI/LitServe/assets/3640001/883b54bd-e54e-497a-8a29-0431abd77695" target="_blank">
        <img src="https://pl-bolts-doc-images.s3.us-east-2.amazonaws.com/app-2/ls_video_banner_3.png" alt="Video Thumbnail" style="width: 2500px; height: auto;" />
      </a>
    </td>
  </tr>
</table>


***💡 TIP: Think of LitServe as [PyTorch Lightning](https://github.com/Lightning-AI/pytorch-lightning) for model serving.***   

&nbsp; 

### Performance  
LitServe (built on FastAPI), is optimized for AI workloads like model serving, embeddings, and LLM serving.

<div align="center">
  <img alt="Lightning" src="https://pl-bolts-doc-images.s3.us-east-2.amazonaws.com/app-2/litserve-perf-2.png" width="1000px" style="max-width: 100%;">
</div>   

These benchmarks are for image and text classification as examples.  Reproduce and read the full benchmarks [here](https://lightning.ai/docs/litserve/home/benchmarks). 

    
***💡 Note on LLM serving:*** For high-performance LLM serving (like Ollama/VLLM, use [LitGPT](https://github.com/Lightning-AI/litgpt?tab=readme-ov-file#deploy-an-llm)) or build your custom VLLM-like server with LitServe. Optimizations like kv-caching, which can be done with LitServe, are needed for best LLM performance.

&nbsp; 

### Featured examples    

<table>
  <tr>
    <td style="vertical-align: top;">
<pre>
<strong>Key features</strong><br>
✅ <strong>Serve all models:  </strong> LLMs, vision, etc
✅ <strong>All ML frameworks: </strong> PyTorch/Jax/sklearn/...
✅ <strong>Developer friendly:</strong> focus on AI, not infra
✅ <strong>Minimal interface: </strong> no abstractions
✅ <strong>Enterprise scale:  </strong> scale huge models
✅ <strong>Auto GPU scaling:  </strong> zero code changes
✅ <strong>Self host:         </strong> or run on Studios
</pre>
    </td>
    <td style="vertical-align: top;">
<pre>
<strong>Featured examples</strong><br>
<strong>Toy model:</strong>  <a href="#define-a-server">Hello world</a>
<strong>LLMs:</strong>       <a href="https://lightning.ai/lightning-ai/studios/openai-fault-tolerant-proxy-server">Llama 3 (8B)</a>, <a href="https://lightning.ai/lightning-ai/studios/deploy-a-voice-clone-api-coqui-xtts-v2-model">LLM Proxy server</a>
<strong>NLP models:</strong> <a href="https://lightning.ai/lightning-ai/studios/deploy-any-hugging-face-model-instantly">Any Hugging face model</a>, <a href="https://lightning.ai/lightning-ai/studios/deploy-a-hugging-face-bert-model">BERT model</a>
<strong>Multimodal:</strong> <a href="https://lightning.ai/lightning-ai/studios/deploy-open-ai-clip-with-litserve">OpenAI Clip</a>
<strong>Audio:</strong>      <a href="https://lightning.ai/lightning-ai/studios/deploy-open-ai-s-whisper-model">OpenAI Whisper</a>, <a href="https://lightning.ai/lightning-ai/studios/deploy-an-music-generation-api-with-meta-s-audio-craft">AudioCraft</a>, <a href="https://lightning.ai/lightning-ai/studios/deploy-an-audio-generation-api">Stable Audio</a>
<strong>Vision:</strong>     <a href="https://lightning.ai/lightning-ai/studios/deploy-a-private-api-for-stable-diffusion-2">Stable diffusion 2</a>
<strong>Speech:</strong>     <a href="https://lightning.ai/lightning-ai/studios/deploy-a-voice-clone-api-coqui-xtts-v2-model">Text-speech (XTTS V2)</a>
</pre>
    </td>
  </tr>
</table>

&nbsp;

# Quick start

Install LitServe via pip (or [advanced installs](https://lightning.ai/docs/litserve/home/install)):

```bash
pip install litserve
```
    
### Define a server    
Here's a hello world example ([explore real examples](https://lightning.ai/docs/litserve/examples)):

```python
# server.py
import litserve as ls

# STEP 1: DEFINE A MODEL API
class SimpleLitAPI(ls.LitAPI):
    # Called once at startup. Setup models, DB connections, etc...
    def setup(self, device):
        self.model = lambda x: x**2  

    # Convert the request payload to model input.
    def decode_request(self, request):
        return request["input"] 

    # Run inference on the the model, return the output.
    def predict(self, x):
        return self.model(x) 

    # Convert the model output to a response payload.
    def encode_response(self, output):
        return {"output": output} 

# STEP 2: START THE SERVER
if __name__ == "__main__":
    api = SimpleLitAPI()
    server = ls.LitServer(api, accelerator="auto")
    server.run(port=8000)
```

Now run the server via the command-line

```bash
python server.py
```

`LitAPI` class gives full control and hackability.    
`LitServer` handles optimizations like batching, auto-GPU scaling, etc...      
    
### Query the server

Use the automatically generated LitServe client or write your own:

<table>
  <tr>
    <td style="vertical-align: top;">
<pre>
<strong>Option A - Use generated client:           </strong><br>
  
```bash
python client.py
```
<br>

</pre>
    </td>
    <td style="vertical-align: top;">
<pre>
<strong>Option B - Custom client example:          </strong><br>

```python
import requests
response = requests.post(
    "http://127.0.0.1:8000/predict",
    json={"input": 4.0}
)
```
<br>
</pre>
    </td>
  </tr>
</table>

&nbsp;

# Deployment options    
LitServe is developed by [Lightning AI](https://lightning.ai/) which provides infrastructure for deploying AI models. Self-manage deployments or use [Lightning Studios](https://lightning.ai/) for production-grade deployments without cloud headaches, security and 99.95% uptime SLA.     

&nbsp;

<div align="center">
<a target="_blank" href="https://lightning.ai/lightning-ai/studios/litserve-hello-world">
  <img src="https://pl-bolts-doc-images.s3.us-east-2.amazonaws.com/app-2/deploy-on-studios.svg" alt="Open In Studio"/>
</a>
</div>

&nbsp;

| Feature                          | Self Managed                      | Fully Managed on Studios            |
|----------------------------------|-----------------------------------|-------------------------------------|
| Deployment                       | ✅ Do it yourself deployment       | ✅ One-button cloud deploy           |
| Load balancing                   | ❌                                | ✅                                  |
| Autoscaling                      | ❌                                | ✅                                  |
| Multi-machine inference          | ❌                                | ✅                                  |
| Authentication                   | ❌                                | ✅                                  |
| Own VPC                          | ❌                                | ✅                                  |
| AWS, GCP                         | ❌                                | ✅                                  |
| Use your own cloud commits       | ❌                                | ✅                                  |


&nbsp;

# Features
LitServe supports multiple advanced state-of-the-art features.

✅ [All model types: LLMs, vision, time series, etc...](https://lightning.ai/docs/litserve/examples).        
✅ [Auto-GPU scaling](https://lightning.ai/docs/litserve/features/gpu-inference).    
✅ [Authentication](https://lightning.ai/docs/litserve/features/authentication).    
✅ [Autoscaling](https://lightning.ai/docs/litserve/features/autoscaling).    
✅ [Batching](https://lightning.ai/docs/litserve/features/batching).    
✅ [Streaming](https://lightning.ai/docs/litserve/features/streaming).    
✅ [All ML frameworks: PyTorch, Jax, Tensorflow, Hugging Face...](https://lightning.ai/docs/litserve/features/full-control).        
✅ [Open AI spec](https://lightning.ai/docs/litserve/features/open-ai-spec).    
[10+ features...](https://lightning.ai/docs/litserve/features).    

**Note:** Our goal is not to jump on every hype train, but instead support features that scale
under the most demanding enterprise deployments.

&nbsp;

# Community
LitServe is a [community project accepting contributions](https://lightning.ai/docs/litserve/community) - Let's make the world's most advanced AI inference engine.

💬 [Get help on Discord](https://discord.com/invite/XncpTy7DSt)    
📋 [License: Apache 2.0](https://github.com/Lightning-AI/litserve/blob/main/LICENSE)    
