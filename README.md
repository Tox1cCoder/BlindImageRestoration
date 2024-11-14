<div align="center">
<h1>Blind Image Restoration with</br>Instant Generative Reference</h1>
</div>

## Usage

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
INSTANTIR_PATH=<path_to_InstantIR> python gradio_demo/app.py
```

Then, visit the local demo via browser at `http://localhost:7860`.

## Reference

```
@article{huang2024instantir,
  title={InstantIR: Blind Image Restoration with Instant Generative Reference},
  author={Huang, Jen-Yuan and Wang, Haofan and Wang, Qixun and Bai, Xu and Ai, Hao and Xing, Peng and Huang, Jen-Tse},
  journal={arXiv preprint arXiv:2410.06551},
  year={2024}
}
```
