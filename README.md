<div align="center">
<h1>Blind Image Restoration with</br>Instant Generative Reference</h1>
</div>

Handling test-time unknown degradation is the major challenge in Blind Image Restoration (BIR), necessitating high model generalization. An effective strategy is to incorporate prior knowledge, either from human input or generative model. In this paper, we introduce Instant-reference Image Restoration (InstantIR), a novel diffusion-based BIR method which dynamically adjusts generation condition during inference. We first extract a compact representation of the input via a pre-trained vision encoder. At each generation step, this representation is used to decode current diffusion latent and instantiate it in the generative prior. The degraded image is then encoded with this reference, providing robust generation condition. We observe the variance of generative references fluctuate with degradation intensity, which we further leverage as an indicator for developing a sampling algorithm adaptive to input quality. Extensive experiments demonstrate InstantIR achieves state-of-the-art performance and offering outstanding visual quality. Through modulating generative references with textual description, InstantIR can restore extreme degradation and additionally feature creative restoration.

<img src='assets/teaser_figure.png'>

### Usage

### 1. Clone this repo and setting up environment

```sh
git clone https://github.com/Tox1cCoder/BlindImageRestoration.git
cd BlindImageRestoration
conda create -n blindir python=3.9 -y
conda activate blindir
pip install -r requirements.txt
```

### 2. Download pre-trained models

| link                                                                    | Python command                                                        
|:------------------------------------------------------------------------|:----------------------------------------------------------------------
| [SDXL](https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0) | `hf_hub_download(repo_id="stabilityai/stable-diffusion-xl-base-1.0")` 
| [facebook/dinov2-large](https://huggingface.co/facebook/dinov2-large)   | `hf_hub_download(repo_id="facebook/dinov2-large")`                    
| [InstantX/InstantIR](https://huggingface.co/InstantX/InstantIR)         | `hf_hub_download(repo_id="InstantX/InstantIR")`                       

### 3. Deploy local gradio demo

```sh
python gradio_demo/app.py
```

Then, visit the local demo via browser at `http://localhost:7860`.
