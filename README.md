<div align="center">
<h1>InstantIR: Blind Image Restoration with</br>Instant Generative Reference</h1>
</div>

## Usage
<!-- ### Online Demo

### Quick start
#### 1. Clone this repo and setting up environment
```sh
git clone https://github.com/JY-Joy/InstantIR.git
cd InstantIR
conda create -n instantir python=3.9 -y
conda activate instantir
pip install -r requirements.txt
```

#### 2. Download pre-trained models

InstantIR is built on SDXL and DINOv2. You can download them either directly from 🤗 huggingface or using Python package.

| 🤗 link | Python command
| :--- | :----------
|[SDXL](https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0) | `hf_hub_download(repo_id="stabilityai/stable-diffusion-xl-base-1.0")`
|[facebook/dinov2-large](https://huggingface.co/facebook/dinov2-large) | `hf_hub_download(repo_id="facebook/dinov2-large")`
|[InstantX/InstantIR](https://huggingface.co/InstantX/InstantIR) | `hf_hub_download(repo_id="InstantX/InstantIR")`

Note: Make sure to import the package first with `from huggingface_hub import hf_hub_download` if you are using Python script.

#### 3. Inference

You can run InstantIR inference using `infer.sh` with the following arguments specified.

```sh
infer.sh \
    --sdxl_path <path_to_SDXL> \
    --vision_encoder_path <path_to_DINOv2> \
    --instantir_path <path_to_InstantIR> \
    --test_path <path_to_input> \
    --out_path <path_to_output>
```

See `infer.py` for more config options. 

#### 4. Using tips

InstantIR is powerful, but with your help it can do better. InstantIR's flexible pipeline makes it tunable to a large extent. Here are some tips we found particularly useful for various cases you may encounter:
- **Over-smoothing**: reduce `--cfg` to 3.0～5.0. Higher CFG scales can sometimes rigid lines or lack of details.
- **Low fidelity**: set `--preview_start` to 0.1~0.4 to preserve fidelity from inputs. The previewer can yield misleading references when input latent is too noisy. In such cases, we suggest to disable the previewer at early timesteps.
- **Local distortions**: set `--creative_start` to 0.6~0.8. This will let InstantIR render freely in the late diffusion process, where the high-frequency details are generated. Smaller `--creative_start` spares more spaces for creative restoration, but will diminish fidelity.
- **Faster inference**: higher `--preview_start` and lower `--creative_start` can both reduce computational costs and accelerate InstantIR inference.

> [!CAUTION]
> These features are training-free and thus experimental. If you would like to try, we suggest to tune these parameters case-by-case.

### Use InstantIR with diffusers 🧨

InstantIR is fully compatible with `diffusers` and is supported by all those powerful features in this package. You can directly load InstantIR via `diffusers` snippet:

```py
# !pip install diffusers opencv-python transformers accelerate
import torch
from PIL import Image

from diffusers import DDPMScheduler
from schedulers.lcm_single_step_scheduler import LCMSingleStepScheduler

from module.ip_adapter.utils import load_adapter_to_pipe
from pipelines.sdxl_instantir import InstantIRPipeline

# suppose you have InstantIR weights under ./models
instantir_path = f'./models'

# load pretrained models
pipe = InstantIRPipeline.from_pretrained('stabilityai/stable-diffusion-xl-base-1.0', torch_dtype=torch.float16)

# load adapter
load_adapter_to_pipe(
    pipe,
    f"{instantir_path}/adapter.pt",
    image_encoder_or_path = 'facebook/dinov2-large',
)

# load previewer lora
pipe.prepare_previewers(instantir_path)
pipe.scheduler = DDPMScheduler.from_pretrained('stabilityai/stable-diffusion-xl-base-1.0', subfolder="scheduler")
lcm_scheduler = LCMSingleStepScheduler.from_config(pipe.scheduler.config)

# load aggregator weights
pretrained_state_dict = torch.load(f"{instantir_path}/aggregator.pt")
pipe.aggregator.load_state_dict(pretrained_state_dict)

# send to GPU and fp16
pipe.to(device='cuda', dtype=torch.float16)
pipe.aggregator.to(device='cuda', dtype=torch.float16)
```

Then, you just need to call the `pipe` and InstantIR will handle your image!

```py
# load a broken image
low_quality_image = Image.open('./assets/sculpture.png').convert("RGB")

# InstantIR restoration
image = pipe(
    image=low_quality_image,
    previewer_scheduler=lcm_scheduler,
).images[0]
```

### Deploy local gradio demo

We provide a python script to launch a local gradio demo of InstantIR, with basic and some advanced features implemented. Start by running the following command in your terminal:

```sh
INSTANTIR_PATH=<path_to_InstantIR> python gradio_demo/app.py
```

Then, visit your local demo via your browser at `http://localhost:7860`.


## ⚙️ Training
