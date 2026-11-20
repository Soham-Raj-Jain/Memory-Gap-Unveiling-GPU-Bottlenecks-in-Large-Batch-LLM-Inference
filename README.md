# Mind the Memory Gap: Unveiling GPU Bottlenecks in Large-Batch LLM Inference

CMPE 297 paper presentation, San Jose State University

**Presenter:** Soham Raj Jain

## About this project

This repo holds my presentation on a 2025 LLM systems paper, *Mind the Memory Gap: Unveiling GPU Bottlenecks in Large-Batch LLM Inference* (Recasens et al., IEEE CLOUD 2025).

The paper challenges a common belief that large batches make LLM inference compute-bound. Using GPU profiling on an NVIDIA H100, the authors show that decoding stays memory-bound even at the largest batch sizes, because the attention step saturates DRAM bandwidth. They also propose a Batching Configuration Advisor (BCA) that picks a smaller batch size near the throughput knee, then uses the freed GPU memory to run extra model replicas for higher overall throughput.

## Links

- **Video walkthrough (YouTube):** YOUR_YOUTUBE_LINK
- **Medium article:** YOUR_MEDIUM_LINK
- **Original paper (arXiv):** https://arxiv.org/abs/2503.08311
- **Authors' code:** https://github.com/FerranAgulloLopez/vLLMBatchingMemoryGap

## What's in this repo

```
.
├── README.md
├── slides/
│   └── Mind_the_Memory_Gap_slides.pptx
├── script.md        # slide-by-slide speaking script (about 5 to 6 minutes)
└── article.md       # text of the Medium article
```

## Summary of the paper

- **The question:** Why does LLM serving throughput flatten as batch size grows?
- **The common assumption:** The workload turns compute-bound at large batches.
- **What they found:** Decoding remains memory-bound. The attention kernel's arithmetic intensity stays flat, so it hits the GPU's memory bandwidth limit while compute sits mostly idle.
- **The fix:** BCA chooses a batch size near the knee point under a latency limit, freeing GPU memory.
- **The payoff:** Model replication on the freed memory raised throughput by about 34% for OPT-1.3B and roughly 7 to 13% for OPT-2.7B, at the cost of higher latency.

## Key takeaways

1. Large-batch decoding is still memory-bound.
2. Past the knee point, bigger batches mostly waste memory.
3. Saved memory can be turned into real throughput through replication.

## Reference

Recasens, et al. "Mind the Memory Gap: Unveiling GPU Bottlenecks in Large-Batch LLM Inference." IEEE CLOUD 2025. arXiv:2503.08311.
