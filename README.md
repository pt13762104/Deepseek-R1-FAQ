Note: All information below are for Q4_K_M unless otherwise stated.
## 1) I have 96/128GB RAM. Can I run Deepseek R1?
To an extent, yes, you actually can (with small quants). The experience is nowhere near "great" (1t/s!), but you can if you allow data to be loaded from disk. See https://www.reddit.com/r/LocalLLaMA/comments/1idseqb/deepseek_r1_671b_over_2_toksec_without_gpu_on/ .
## 2) Are distilled models "R1"?
No.
## 3) What are the system requirements?
| **Model** | **Minimum VRAM** | **Recommended VRAM** | **Minimum RAM** | **Recommended RAM** | **KV cache size MB (2k context)** | **Example hardware** |
|-----------|------------------|----------------------|-----------------|---------------------|-----------------------------------|----------------------|
| 671b      | 480              | 640                  | 512             | 768                 | 9760                              | 8x H100              |
## 4) I have 8 channels of RAM, how many token/s can I expect?
Expect about 4-6 token/s for DDR5, 3-4 for DDR4.
## 5) Can you get an usable R1 experience without GPUs?
With multi-channel RAM (12+ channels, 768 bit bus or more) you can get >= 10t/s if your RAM is clocked high enough. It should be usable if you have enough of that kind of RAM.
## 6) If I don't have the resources, should I run the setup in 1)?
I don't think so, at least it's not quite worth it if you're not going to wait.
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
