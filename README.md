<div align="center">
 👋 Hi, everyone! 
    <br>
    We are <b>ByteDance Seed team.</b>
</div>

<p align="center">
  You can get to know us better through the following channels👇
  <br>
  <a href="https://team.doubao.com/">
    <img src="https://img.shields.io/badge/Website-%231e37ff?style=for-the-badge&logo=bytedance&logoColor=white"></a>
  <a href="https://github.com/user-attachments/assets/93481cda-a7f3-47f3-b333-fe6b3da86b78">
    <img src="https://img.shields.io/badge/WeChat-07C160?style=for-the-badge&logo=wechat&logoColor=white"></a>
 <a href="https://www.xiaohongshu.com/user/profile/668e7e15000000000303157d?xsec_token=ABl2-aqekpytY6A8TuxjrwnZskU-6BsMRE_ufQQaSAvjc%3D&xsec_source=pc_search">
    <img src="https://img.shields.io/badge/Xiaohongshu-%23FF2442?style=for-the-badge&logo=xiaohongshu&logoColor=white"></a>
  <a href="https://www.zhihu.com/org/dou-bao-da-mo-xing-tuan-dui/">
    <img src="https://img.shields.io/badge/zhihu-%230084FF?style=for-the-badge&logo=zhihu&logoColor=white"></a>
</p>

![seed logo](https://github.com/user-attachments/assets/c42e675e-497c-4508-8bb9-093ad4d1f216)


## 🚀 Mopenhands: Multi-SWE-Bench Infer with OpenHands
<p align="center">
  <a href="https://github.com/multi-swe-bench/multi-swe-bench">
    <img src="https://img.shields.io/badge/Multi_SWE_bench-Project Page-yellow"></a>
  <a href="https://arxiv.org/pdf/2502.19811">
    <img src="https://img.shields.io/badge/Multi_SWE_bench-Tech Report-red"></a>
  <a href="https://huggingface.co/datasets/bytedance-research/Multi-SWE-Bench">
    <img src="https://img.shields.io/badge/Multi_SWE_bench-Hugging Face-orange"></a>
  <br>
  <a href="https://huggingface.co/Multi-SWE-RL">
    <img src="https://img.shields.io/badge/Multi_SWE_RL_Community-Hugging Face-EE9A12"></a>
  <a href="https://discord.gg/EtfbkfqUuN">
    <img src="https://img.shields.io/badge/Multi_SWE_RL_Community-Discord-1449DA"></a>
  <a href="https://github.com/multi-swe-bench/multi-swe-bench/blob/main/LICENSE">
    <img src="https://img.shields.io/badge/License-Apache-blue"></a>
</p>

We have modified the original [**Openhands**](https://github.com/All-Hands-AI/OpenHands) (0.25.0 version) compatible with [**Multi-SWE-Bench**](https://github.com/multi-swe-bench/multi-swe-bench)! MopenHands can be used to evaluate the performance of LLMs across 7 languages(c++, c, java, go, rust, typescript, javascript) in the [**Multi-SWE-Bench** dataset](https://huggingface.co/datasets/bytedance-research/Multi-SWE-Bench).


## To Start
### 1. Environment Preparing
```bash
conda create -n openhands python=3.12 conda-forge::nodejs conda-forge::poetry
conda activate openhands
make build
```
Make sure you have docker environment in your local device
You should first create a file named config.toml, and update your model key in the file, for example:
```bash
[llm.YYY]
model = "llm.xxx"
base_url = "xxx"
api_key = "xxx"
```

### 2. Dataset Preparing
You should first download the [**Multi-SWE-Bench** dataset](https://huggingface.co/datasets/bytedance-research/Multi-SWE-Bench).
And change the dataset following /evaluation/benchmarks/swe_bench/data/data_change.py


## Run Inference on SWE-Bench Instances

```bash
bash evaluation/benchmarks/swe_bench/infer.sh
```
### Explanation

- `models`, e.g. `llm.eval_gpt4_1106_preview`, is the config group name for your
LLM settings, as defined in your `config.toml`.
- `git-version`, e.g. `HEAD`, is the git commit hash of the OpenHands version you would
like to evaluate. It could also be a release tag like `0.6.2`.
- `agent`, e.g. `CodeActAgent`, is the name of the agent for benchmarks, defaulting to `CodeActAgent`.
- `eval_limit`, e.g. `10`, limits the evaluation to the first `eval_limit` instances. By
default, the script evaluates the (500 issues), which will no exceed the maximum of the dataset number.
- `max_iter`, e.g. `20`, is the maximum number of iterations for the agent to run. By
default, it is set to 50.
- `num_workers`, e.g. `3`, is the number of parallel workers to run the evaluation. By
default, it is set to 1.
- `language`, the language of your evaluating dataset.
- `dataset`, the absolute position of the dataset jsonl.

### Images
We provide the images for each instance. You can use the following command to download the images directly from [our docker hub site](https://hub.docker.com/repositories/mopenhands0) rather than build them locally.

## 📊 Evaluation
After running the agent, all the predicted patches will be save in `evaluation/evaluation_outputs` directory, named as `output.jsonl`. You can extract the `git_patch` of each instance and then you can evaluate in the [multi-swe-bench](https://github.com/multi-swe-bench/multi-swe-bench) repo

### Run Evaluation

To run the evaluation, you need to prepare the following:

1. Patch Files: Some patch files in JSONL format, each item containing:
   - `org`: Organization Name
   - `repo`: Repository Name
   - `number`: Pull Request Number
   - `fix_patch`: Fix Patch Content
2. Dataset Files: Dataset files in JSONL format available on Hugging Face, such as [Multi-SWE-Bench](https://huggingface.co/datasets/Multi-SWE-RL/Multi-SWE-Bench)

Then you can run the evaluation using the following command:

```bash
cd multi-swe-bench
python -m multi_swe_bench.harness.run_evaluation --config /path/to/your/config.json
```

## 📜 License
This project is licensed under Apache License 2.0. See the [LICENSE](/LICENSE) flie for details.
## 📖 Citation
If you find our Multi-SWE-bench and MopenHands useful for your research and applications, feel free to give us a star ⭐ or cite us using:

```bibtex
@misc{zan2025multiswebench,
      title={Multi-SWE-bench: A Multilingual Benchmark for Issue Resolving}, 
      author={Daoguang Zan and Zhirong Huang and Wei Liu and Hanwu Chen and Linhao Zhang and Shulin Xin and Lu Chen and Qi Liu and Xiaojian Zhong and Aoyan Li and Siyao Liu and Yongsheng Xiao and Liangqiang Chen and Yuyu Zhang and Jing Su and Tianyu Liu and Rui Long and Kai Shen and Liang Xiang},
      year={2025},
      eprint={2504.02605},
      archivePrefix={arXiv},
      primaryClass={cs.SE},
      url={https://arxiv.org/abs/2504.02605}, 
}
```
## 🏢 About [ByteDance Seed Team](https://team.doubao.com/)

Founded in 2023, ByteDance Seed Team is dedicated to crafting the industry's most advanced AI foundation models. The team aspires to become a world-class research team and make significant contributions to the advancement of science and society.
