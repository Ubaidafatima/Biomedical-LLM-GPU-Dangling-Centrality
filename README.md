# Biomedical LLM GPU Dangling Centrality

Reproducibility package for GPU-accelerated graph-theoretic auditing of biomedical LLM attention graphs.

## Main result

On **150 held-out BioGPT/MedMCQA attention graphs**, batched CUDA (microbatch size 32) accelerated the exact Dangling Centrality graph-auditing workload by **15.62x** relative to an algorithmically matched NumPy CPU implementation. The maximum numerical discrepancy across implementations was **2.74e-6**.

The **15.62x result applies to the graph-auditing stage**. When the common BioGPT inference / graph-construction cost is included in a component-summed pipeline estimate, batched CUDA yields a **1.107x pipeline speedup**, corresponding to a **9.67% time reduction**.

## Experimental design

- Biomedical dataset: MedMCQA validation questions
- Language model: BioGPT
- Calibration set: 50 real attention graphs
- Held-out evaluation set: 150 real attention graphs
- Selected CUDA microbatch size: 32
- Adaptive CPU/GPU crossover: 23 nodes
- Hardware used for the reported benchmark: NVIDIA A100-SXM4-40GB
- Backends: NetworkX CPU, matched NumPy CPU, ordinary CUDA/CuPy, batched CUDA/CuPy, adaptive CPU/CUDA

Calibration-only tuning was completed before the 150 held-out graphs were evaluated.

## Repository structure

```text
notebooks/
  00_networkx_vs_cuda_200q_context.ipynb
  01_matched_numpy_cpu_vs_cuda_gpu.ipynb
  02_batched_cuda_adaptive_cpu_gpu.ipynb
results/
  heldout_150_backend_summary.csv
  component_summed_pipeline_summary.csv
  summary.json
docs/
  GTC_2027_vector_poster_draft.pdf
CITATION.cff
requirements.txt
```

## Reproduction

1. Use a CUDA-capable NVIDIA GPU environment.
2. Install the Python dependencies in `requirements.txt`. Use a CuPy package/build compatible with the CUDA runtime on the system.
3. Run `notebooks/01_matched_numpy_cpu_vs_cuda_gpu.ipynb` to verify algorithmic fairness between matched NumPy CPU and CUDA/CuPy.
4. Run `notebooks/02_batched_cuda_adaptive_cpu_gpu.ipynb` for calibration, batching, adaptive routing, and held-out evaluation.
5. Compare generated outputs with the summary files in `results/`.

## Key benchmark summary

| Backend | 150-graph runtime (s) | Throughput (graphs/s) | Speedup vs NumPy |
|---|---:|---:|---:|
| NumPy CPU | 0.8669 | 173.03 | 1.00x |
| Ordinary CUDA (batch=1) | 0.4167 | 359.97 | 2.08x |
| Batched CUDA (batch=32) | 0.0555 | 2702.04 | 15.62x |
| Adaptive CPU/CUDA (T=23) | 0.0569 | 2634.49 | 15.23x |

## Prior work underlying Dangling Centrality

1. U. Fatima, S. Hina, and M. Wasif, “Dangling Centrality Highlights Critical Nodes by Evaluating Network Stability Through Link Removal,” *Scientific Reports*, 15, 41078, 2025. DOI: 10.1038/s41598-025-24930-8.
2. U. Fatima, “A Theoretically Informed Dangling Centrality (phi_C) Metric Across Sparse and Large-Scale Networks,” *Data Intelligence*, 8, Art. 20260100, 2026. DOI: 10.3724/2096-7004.di.2026.0100.
3. U. Fatima and T. Ahsan, “A Novel Dangling Centrality Metric for Real-Life Quantum Graphs with Applications in Control Systems,” *IEEE QAI*, pp. 466-472, 2025. DOI: 10.1109/QAI63978.2025.00078.

## Citation

Until a Zenodo DOI is minted, cite the repository as:

> U. Fatima and M. Ali, “Biomedical LLM GPU Dangling Centrality: Reproducibility Code and Benchmarks,” GitHub repository, 2026.

After creating a GitHub release and archiving it with Zenodo, replace this temporary citation with the Zenodo DOI.

## License

No license is included automatically. Choose a license before public release if you want others to have explicit reuse rights.
