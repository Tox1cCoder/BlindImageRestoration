<div align="center">
<h1>InstantIR: Blind Image Restoration with</br>Instant Generative Reference</h1>
</div>

## Usage
### Online Demo

### Quick start
#### 1. Clone this repo and setting up environment
```sh
git clone https://github.com/JY-Joy/InstantIR.githttps://github.com/Tox1cCoder/BlindImageRestoration.git
cd InstantIR
conda create -n instantir python=3.9 -y
conda activate instantir
pip install -r requirements.txt
```
#### 2. Download pre-trained models

| link | Python command
| :--- | :----------
|[SDXL](https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0) | `hf_hub_download(repo_id="stabilityai/stable-diffusion-xl-base-1.0")`
|[facebook/dinov2-large](https://huggingface.co/facebook/dinov2-large) | `hf_hub_download(repo_id="facebook/dinov2-large")`
|[InstantX/InstantIR](https://huggingface.co/InstantX/InstantIR) | `hf_hub_download(repo_id="InstantX/InstantIR")`

Note: Make sure to import the package first with `from huggingface_hub import hf_hub_download` if you are using Python script.

#### 3. Inference
