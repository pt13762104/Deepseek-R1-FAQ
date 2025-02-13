Note: All information below are for Q4_K_M and peak llama.cpp token gen performance unless otherwise stated.
## -1) I CAN RUN R1 ON MY RASPBERRY PI / RTX 4090 / MY MOBILE PHONE / ...
See 2) and ~~SHUT UP~~ fix your content, please.
## 0) How do you actually run R1?
Use [Ollama](https://ollama.com) if you want a simple setup. Be sure to pull the `deepseek-r1:671b` model. You can always download quants and run them using [llama-server](https://github.com/ggerganov/llama.cpp).
## 1) I have 96/128GB RAM. Can I run Deepseek R1?
To an extent, yes, you actually can (with small quants e.g. IQ1, Q2, etc...). The experience is nowhere near "great" (1t/s!), but you can if you allow data to be loaded from disk. See https://www.reddit.com/r/LocalLLaMA/comments/1idseqb/deepseek_r1_671b_over_2_toksec_without_gpu_on/. Use a disk that's as fast as possible.
## 2) Are distilled models "R1"?
No.
## 3) What are the system requirements?
| **Model** | **Minimum VRAM** | **Recommended VRAM** | **Minimum RAM** | **Recommended RAM** | **KV cache size MiB (2k context)** | **Example hardware** |
|-----------|------------------|----------------------|-----------------|---------------------|-----------------------------------|----------------------|
| 671b      | 480              | 640                  | 512             | 768                 | 9760                              | 8x H100              |

For max context (160K), you'll need 762.5 GiB of additional RAM/VRAM.
## 4) I have 8 channels of RAM, how many token/s can I expect?
Expect about 4-6 token/s for DDR5, 3-4 for DDR4.
## 5) Can you get an usable R1 experience without GPUs?
With multi-channel RAM (12+ channels, 768 bit bus or more) you can get >= [8t/s](https://www.youtube.com/watch?v=wKZHoGlllu4) peak (only Q4_K_S, sorry) if your RAM is clocked high enough. It should be usable if you have enough of that kind of RAM.
## 6) If I don't have the resources, should I run the setup in 1)?
If you're going to wait for a really long time for a prompt, then maybe.
## 7) How can I run R1 for cheap?
See https://digitalspaceport.com/how-to-run-deepseek-r1-671b-fully-locally-on-2000-epyc-rig/ .
## 8) I have 8xH100s, how many token it's expected?
Around 30 to 40 tokens per second is expected.
## 9) How do I increase throughput?
0. Use a fast enough GPU.
1. Make your RAM faster (obvious)
2. Change used_expert_count to a smaller amount than 8. You might get bad results with a small number of experts.
3. Use KV cache quant.
## 10) My prompt processing speed is slow. Why?
Either use a GPU or add more CPU cores. CPUs don't have big compute power, so they don't do prompts well.
## 11) Can I run R1 on my laptop?
See 1). You can run distributed inference, which should be okay if you have enough RAM bandwidth.
## 11.5) Can you actually run R1 on 4090s?
See 3). You'll need server/workstation CPUs to handle the big number of GPUs.
## 12) My disk space isn't enough!
If your network is really fast, you can download the model to shared memory then run directly from it. This works best on Kaggle (although you shouldn't run models on Kaggle's CPUs).
## 13) Why is the KV cache so big :sob:
Multi head attention, see here: https://github.com/ggerganov/llama.cpp/pull/11446. When MLA is implemented it should reduce the KV size, at the cost of slower prompt processing.
## 14) The model doesn't think in the \<think\> tags!
This is an observed behaviour, see this for more information: https://huggingface.co/deepseek-ai/DeepSeek-R1#usage-recommendations.
