# COVID-19 EHR Benchmark - Online Platform

The repository is a practical implementation of the arXiv paper: ["A Comprehensive Benchmark for COVID-19 Predictive Modeling Using Electronic Health Records in Intensive Care"](https://doi.org/10.48550/arxiv.2209.07805) authored by Junyi Gao*, Yinghao Zhu*, Wenqing Wang*, Yasha Wang, Wen Tang, Ewen M. Harrison, and Liantao Ma.
*\*Equal contribution*

## Introduction

The COVID-19 EHR Benchmark is a comprehensive platform for predictive modeling using Electronic Health Records (EHR) in Intensive Care Units (ICUs). This benchmarking effort is the first of its kind for patient-level COVID-19 prediction tasks in ICUs. The main goal is to provide a reliable and standardized benchmark for researchers and practitioners in the field.

## Features

- **Performance Table**: Provides the average score across all folds. [View Here](https://pyehr.netlify.app/performance-10fold)
- **Detailed Performance Table**: Includes comprehensive performance details for each fold. [View Here](https://pyehr.netlify.app/performance-all)
- **Checkpoints & Logs**: Access all model checkpoints and logs. [Access via Google Drive](https://drive.google.com/file/d/1Fdt8XUnO3CeJk9mrkPZBk_gUdpCnGFfi/view)

## Background

To the best of our knowledge, this is the first benchmarking effort for patient-level COVID-19 prediction tasks in ICUs. We have made our code publicly available, enabling others to build complete benchmarks and reproduce all results. Our well-structured data preprocessing and modeling modules can also be easily applied to generate customized tasks and results. The benchmark code and documentations can be accessed at [GitHub Repository](https://github.com/yhzhu99/pyehr). Moreover, we have released all the benchmark experiment results and trained models on this online platform, which includes model performances with all hyperparameter combinations for both tasks and makes the results easy to query and download. Further details on data and code availability, including the benchmark code structure, are provided in Supplementary Materials.

## Access

The platform can be accessed at [https://pyehr.netlify.app](https://pyehr.netlify.app).

## License

This project is licensed under the terms of the MIT license. See [LICENSE](LICENSE) for additional details.

## Contributors

This project is brought to you by the following contributors:

- [Yinghao Zhu](https://github.com/yhzhu99)
- [Wenqing Wang](https://github.com/ericaaaaaaaa)
- [Junyi Gao](https://github.com/v1xerunt)
- [Hao Li](https://github.com/LLLeoLi)


For a deeper dive into our research, please refer to our [paper](https://doi.org/10.48550/arxiv.2209.07805).

```
@misc{gao2023comprehensive,
      title={A Comprehensive Benchmark for COVID-19 Predictive Modeling Using Electronic Health Records in Intensive Care}, 
      author={Junyi Gao and Yinghao Zhu and Wenqing Wang and Yasha Wang and Wen Tang and Ewen M. Harrison and Liantao Ma},
      year={2023},
      eprint={2209.07805},
      archivePrefix={arXiv},
      primaryClass={cs.LG}
}
```

## Contribution

We welcome contributions from the community. If you find any issues or have suggestions, please raise them in the GitHub repository.
