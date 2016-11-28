---
layout: post
title: ISCA 2011 Energy-efficient Mechanisms for Managing Thread Context in Throughput Processors
date: 2016-11-20
tags: Register File, GPU
---
## Summary

This paper proposed register file cache, which contains the immediate register working set of active threads, and a two-level scheduler to maintain a small set of active thread for ALU and local memory latency and a larger set of pending threads for global memory latency. 6-entry per thread register file cache can reduce read and write to main register file with 50% and 59%. They can further reduce count of active thread at a factor of 4, which have minimal impact of performance and reduce 36% reduction of register file energy.

## Baseline and Facts

* Baseline: 16 SM, 32 SIMT lane, 6 high bandwidth DRAM channels, on-chip L2 cache and 128KB register file per SM.
* Register file consumes 10% of total GPU power in GTX280.

## Major Design
* register file cache: 6 entries per thread.
	* equals to 24KB per SM, 1/5 size of MRF if no scheduler assistance.
	* RFC only allocated to active warps. RFC now is 21x smaller than MRF, RFC supports 8 warps per SM.
* 2-level warp scheduler:
	* hide two latency: long unpredictable latency / shorter fixed latency
	* active set could be 6-8 and this setting has negligible impact on performance.

## Energy savings
* MRF traffic reduction:
	* 4,6,8 active warps with 4,6,8 RFC entries per thread
	* 6 RFC and 8 active warps reduces energy by 25% without performance penalty. Idealize would be 58%.
	* save (36%) 3.3 watt total chip without affecting performance.

## Key Points
* Static liveness information can be used to elide writing dead value back from the register file cache to main register file.
