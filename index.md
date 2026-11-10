---
layout: default
title: Methodology Assignment 4
---

# Abhinav Chinnam

**Email:** achinnam@ucsd.edu  
**Section:** D39 – Quantization in LLMs  
**Mentor:** Arya Mazumdar

---

**What is the most interesting topic covered in your domain this quarter?**

The most interesting topic for me was the structure of the KV cache that the researchers discovered within the KIVI paper. They observed how the keys have a handful of *outlier channels* where certain columns or dimensions that are much larger than the rest across all tokens. They also observed how values have no such outlier structure. So what they noticed was that quantization for the keys per token was actually quite poor, since one outlier channel would inflate the scale. The researchers decided to quantize keys per channel and values per token. We were able to verify this ourselves on Qwen3-1.7B, which was pretty neat.

**Describe a potential investigation you would like to pursue for your Quarter 2 Project.**

One potential investigation that I want to look into would be an a benchmark of quantization methods for running small LLMs on consumer hardware. Many people would like to run models on their own laptops for privacy or cost reasons. But it isn't entirely clear which quantization choices give the best trade-offs on limited memory. So our group could potentilly look at a few small, but high performing open models and compare common quantization approaches. For each of the combinations of model and quantization approach, we could measure output quality via standard tasks like GSM8K or a small LongBench subset, along with practical metrics like time to first token. 

**What is a potential change you'd make to the approach in your current Quarter 1 Project?**

As of right now, we have mostly evaluated KIVI offline, where we save one KV cache from a single forward pass, fake-quantize it, and measure reconstruction and attention errors against the true cache values. What we need to continue on would be evaluation in a streaming setting, where we would be able to actually observe error propogation through the layers of our llm. I think it's also important for us to be careful to separate accuracy effects from memory effects, since we want to understand the real memory and speed benefits. 

**What other techniques would you be interested in using in your project?**

Some other techniques that would be cool to see within our project would be evaluation beyond LongBench, maybe more general purpose benchmarks to see how quantization affects output quality. Some other methods could be GPU kernel work for inference acceleration. Writing a custom kernel that stores the cache and dequantizes it on the fly during attention would let us measure real latency and throughput, along with memory savings. 
