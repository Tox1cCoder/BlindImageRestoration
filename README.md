<div align="center">
<h1>InstantIR: Blind Image Restoration with</br>Instant Generative Reference</h1>
</div>

## Usage
### Online Demo

### Quick start
#### 1. Clone this repo and setting up environment
```sh
git clone https://github.com/Tox1cCoder/BlindImageRestoration.git
cd BlindImageRestoration
conda create -n blindir python=3.9 -y
conda activate blindir
pip install -r requirements.txt
```
#### 2. Download pre-trained models

| link | Python command
| :--- | :----------
|[SDXL](https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0) | `hf_hub_download(repo_id="stabilityai/stable-diffusion-xl-base-1.0")`
|[facebook/dinov2-large](https://huggingface.co/facebook/dinov2-large) | `hf_hub_download(repo_id="facebook/dinov2-large")`
|[InstantX/InstantIR](https://huggingface.co/InstantX/InstantIR) | `hf_hub_download(repo_id="InstantX/InstantIR")`

#### 3. Inference
