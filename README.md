<p align="center">
  <img width="225" src=".github/logo.png">
</p>

<h2 align="center">UniPixel: Unified Object Referring and Segmentation<br>for Pixel-Level Visual Reasoning</h2>

<p align="center">
  <a href="https://arxiv.org/abs/2509.18094" target="_blank"><img src="https://img.shields.io/badge/arXiv-2509.18094-red"></a>
  <a href="https://polyu-chenlab.github.io/unipixel/" target="_blank"><img src="https://img.shields.io/badge/Project-Page-brightgreen"></a>
  <a href="https://huggingface.co/collections/PolyU-ChenLab/unipixel-68cf7137013455e5b15962e8" target="_blank"><img src="https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Collection-orange"></a>
  <a href="https://modelscope.cn/datasets/yeliudev/UniPixel-SFT-1M" target="_blank"><img src="https://img.shields.io/badge/%E2%9A%A1%20ModelScope-Dataset-725AFB"></a>
  <a href="https://huggingface.co/spaces/PolyU-ChenLab/UniPixel" target="_blank"><img src="https://huggingface.co/datasets/huggingface/badges/resolve/main/open-in-hf-spaces-sm-dark.svg"></a>
</p>

<p align="center">
  <a href="https://yeliu.dev/">Ye Liu</a><sup>1,2</sup>, <a href="https://scholar.google.com/citations?user=qtdueToAAAAJ">Zongyang Ma</a><sup>2,3</sup>, <a href="https://pujunfu.github.io/">Junfu Pu</a><sup>2</sup>, <a href="https://zhongangqi.github.io/">Zhongang Qi</a><sup>4</sup>, <a href="https://scholar.google.com/citations?user=T-HaQ84AAAAJ">Yang Wu</a><sup>5</sup>, <a href="https://scholar.google.com/citations?user=4oXBp9UAAAAJ">Ying Shan</a><sup>2</sup>, <a href="https://web.comp.polyu.edu.hk/chencw/">Chang Wen Chen</a><sup>1*</sup>
  <p align="center"><sup>1</sup>The Hong Kong Polytechnic University <sup>2</sup>ARC Lab, Tencent PCG<br/><sup>3</sup>Chinese Academy of Sciences <sup>4</sup>vivo Mobile Communication Co. <sup>5</sup>Tencent AI Lab</p>
</p>

**UniPixel** is a unified MLLM for pixel-level vision-language understanding. It flexibly supports a variety of fine-grained tasks, including image/video segmentation, regional understanding, and a novel PixelQA task that jointly requires object-centric referring, segmentation, and question-answering in videos.

<p align="center"><img width="750" src=".github/method.jpg"></p>

## 🔥 News

- **`2025.10.03`** 🕹️ Our online demo is available on [Hugging Face Spaces](https://huggingface.co/spaces/PolyU-ChenLab/UniPixel). Enjoy!
- **`2025.09.27`** 🎮 Try our model on custom data [in one click](#-inference-on-custom-data).
- **`2025.09.21`** 🔮 Code, model, and dataset release.
- **`2025.09.18`** 🎉 Our paper has been accepted by [NeurIPS 2025](https://nips.cc/).

## 🏆 UniPixel on Public Benchmarks

| Benchmark                      | Evaluation Results (3B/7B)                                 |
|--------------------------------|------------------------------------------------------------|
| `CT` ReVOS (val)               | `J: 59.7/61.7` `F: 64.4/65.7` `J&F: 62.1/63.7`             |
| `CT` MeViS (val)               | `J: 50.4/53.2` `F: 55.7/58.3` `J&F: 53.1/55.8`             |
| `CT` Ref-YouTube-VOS (val)     | `J: 68.6/69.5` `F: 72.3/72.4` `J&F: 70.5/71.0`             |
| `CT` Ref-DAVIS17 (val)         | `J: 70.7/72.7` `F: 77.8/80.1` `J&F: 74.2/76.4`             |
| `CT` Ref-SAV (val)             | `J: 66.9/68.5` `F: 67.6/69.6` `J&F: 67.2/69.0`             |
| `CT` GroundMoRe (test)         | `J: 36.0/36.5` `F: 38.7/39.1` `J&F: 37.4/37.8`             |
| `CT` RefCOCO (RES)             | `val: 80.5/80.8` `testA: 82.6/83.0` `testB: 76.9/77.4`     |
| `CT` RefCOCO+ (RES)            | `val: 74.3/75.3` `testA: 78.9/80.1` `testB: 68.4/70.0`     |
| `CT` RefCOCOg (RES)            | `val(U): 76.3/76.4` `test(U): 77.0/77.1`                   |
| `CT` ReasonSeg (val)           | `gIoU: 64.0/60.5` `cIoU: 56.2/58.7`                        |
| `CT` VideoRefer-Bench-D        | `single-frame: 3.42/3.37` `multi-frame: 3.44/3.36`         |
| `CT` VideoRefer-Bench-Q        | `single-frame: 72.2/73.4` `multi-frame: 72.8/74.1`         |
| `ZS` MVBench                   | `Acc: 62.5/64.3`                                           |

`CT` and `ZS` refer to multi-task co-training and zero-shot settings, respectively. Evaluation results under more settings can be found in our paper.

## 🕹️ Gradio Demo

🌾 Turn on your sound and enjoy the BGM from [Stardew Valley](https://www.stardewvalley.net/)!

https://github.com/user-attachments/assets/e9a2cb93-7800-4e7a-a452-75adea83dbfb

Play with our demo [online](https://huggingface.co/spaces/PolyU-ChenLab/UniPixel) or see [DEMO.md](/docs/DEMO.md) for guidelines about how to deploy it locally.

## 🎮 Inference on Custom Data

1. Make sure you have [setup the environment](/docs/TRAIN.md#-environment-setup).

2. Run the following script for image or video segmentation.

```shell
# Set the Python Path
export PYTHONPATH="./:$PYTHONPATH"

# Run inference on custom data
python tools/inference.py <media-path> <prompt>

# Example: python tools/inference.py example.jpg 'Please segment the rabbit'
```

Here, `<media-path>` could be a path to an image, a video, or a folder containing video frames (001.jpg, 002.jpg).

<details>
<summary>Here are some example prompts</summary>

```
1. Please segment the tallest giraffe.
2. Where is the nearest sheep? Please provide the segmentation mask.
3. Why is the boy crying? Please provide the segmentation mask and explain why.
4. Who shooted the ball? Please answer the question and provide the segmentation mask.
5. Please segment the object according to the description: <a-long-description>
```
</details>

## 💻 Model Zoo

| Model | Base MLLM | Mask Decoder | Checkpoint | Training Log |
|:-:|:-:|:-:|:-:|:-:|
| UniPixel-3B | [Qwen2.5-VL-3B-Instruct](https://huggingface.co/Qwen/Qwen2.5-VL-3B-Instruct) | [SAM2.1-Hiera-Base+](https://dl.fbaipublicfiles.com/segment_anything_2/092824/sam2.1_hiera_base_plus.pt) | [🤗 Link](https://huggingface.co/PolyU-ChenLab/UniPixel-3B) | [🤗 Link](https://huggingface.co/PolyU-ChenLab/UniPixel-3B/resolve/main/trainer_state.json) |
| UniPixel-7B | [Qwen2.5-VL-7B-Instruct](https://huggingface.co/Qwen/Qwen2.5-VL-7B-Instruct) | [SAM2.1-Hiera-Base+](https://dl.fbaipublicfiles.com/segment_anything_2/092824/sam2.1_hiera_base_plus.pt) | [🤗 Link](https://huggingface.co/PolyU-ChenLab/UniPixel-7B) | [🤗 Link](https://huggingface.co/PolyU-ChenLab/UniPixel-7B/resolve/main/trainer_state.json) |

## 📦 UniPixel-SFT-1M Dataset

We provide raw images/videos and pre-processed annotations of **23 referring/segmentation/QA datasets**, including our **UniPixel-SFT-1M** for training and multiple benchmarks for evaluation. The list of source datasets is shown below. See our [dataset repo](https://huggingface.co/datasets/PolyU-ChenLab/UniPixel-SFT-1M) for more details.

<p align="center"><img width="650" src=".github/dataset.png"></p>

## 🚀 Training

Our codebase supports training and evaluating on [23 datasets and benchmarks](https://github.com/PolyU-ChenLab/UniPixel/blob/main/unipixel/dataset/sub_classes) with the following features.

- Flexible hardware settings: NVIDIA GPU / Ascend NPU, Single-Node / Multi-Node
- Efficient training techniques: DeepSpeed ZeRO, BF16, LoRA, SDPA, FlashAttention2, Liger-Kernel
- Customizing the base LLM and conversation templates
- Monitoring the training process via Tensorboard / Wandb
- Group sampling for mixed dataset training
- Multi-process / multi-device evaluation on public benchmarks

See [TRAIN.md](/docs/TRAIN.md) for a quick start guide.

## 🔮 Evaluation

See [EVAL.md](/docs/EVAL.md) for details about evaluating UniPixel on public benchmarks.

## 📖 Citation

Please kindly cite our paper if you find this project helpful.

```bibtex
@inproceedings{liu2025unipixel,
  title={UniPixel: Unified Object Referring and Segmentation for Pixel-Level Visual Reasoning},
  author={Liu, Ye and Ma, Zongyang and Pu, Junfu and Qi, Zhongang and Wu, Yang and Ying, Shan and Chen, Chang Wen},
  booktitle={Advances in Neural Information Processing Systems (NeurIPS)},
  year={2025}
}
```
