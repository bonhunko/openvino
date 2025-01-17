# Optimizing models post-training {#pot_introduction}

@sphinxdirective

.. toctree::
   :maxdepth: 1
   :hidden:

   Quantizing Model <pot_default_quantization_usage>
   Quantizing Model with Accuracy Control <pot_accuracyaware_usage>
   Quantization Best Practices <pot_docs_BestPractices>
   API Reference <pot_compression_api_README>
   Command-line Interface <pot_compression_cli_README>
   Examples <pot_examples_description>
   pot_docs_FrequentlyAskedQuestions

@endsphinxdirective


Post-training model optimization is the process of applying special methods without model retraining or fine-tuning. Therefore, it does not require either a training dataset or a training pipeline in the source DL framework. In OpenVINO, post-training methods, such as post-training 8-bit quantization, require:
* A floating-point precision model (FP32 or FP16), converted to the OpenVINO IR format (Intermediate Representation)
and run on CPU with OpenVINO.
* A representative calibration dataset representing a use case scenario, for example, 300 samples.
* In case of accuracy constraints, a validation dataset and accuracy metrics should be available.

OpenVINO provides a Post-training Optimization Tool (POT) that supports the uniform integer quantization method. It can substantially increase inference performance and reduce the size of a model.

The figure below shows the optimization workflow with POT:
![](./images/workflow_simple.png)


## Quantizing models with POT

Depending on your needs and requirements, POT provides two main quantization methods that can be used:

*  [Default Quantization](@ref pot_default_quantization_usage) -- a recommended method that provides fast and accurate results in most cases. It requires only an unannotated dataset for quantization. For more details, see the [Default Quantization algorithm](@ref pot_compression_algorithms_quantization_default_README) documentation.

*  [Accuracy-aware Quantization](@ref pot_accuracyaware_usage) -- an advanced method that allows keeping accuracy at a predefined range, at the cost of performance improvement, when `Default Quantization` cannot guarantee it. This method requires an annotated representative dataset and may require more time for quantization. For more details, see the
[Accuracy-aware Quantization algorithm](@ref accuracy_aware_README) documentation.

Different hardware platforms support different integer precisions and quantization parameters. For example, 8-bit is used by CPU, GPU, VPU, and 16-bit by GNA. POT abstracts this complexity by introducing a concept of the "target device" used to set quantization settings, specific to the device.

> **NOTE**: There is a special `target_device: "ANY"` which leads to portable quantized models compatible with CPU, GPU, and VPU devices. GNA-quantized models are compatible only with CPU.

For benchmarking results collected for the models optimized with the POT tool, refer to the [INT8 vs FP32 Comparison on Select Networks and Platforms](@ref openvino_docs_performance_int8_vs_fp32).

## Additional Resources

* [Performance Benchmarks](https://docs.openvino.ai/latest/openvino_docs_performance_benchmarks_openvino.html)
* [INT8 Quantization by Using Web-Based Interface of the DL Workbench](https://docs.openvino.ai/latest/workbench_docs_Workbench_DG_Int_8_Quantization.html)
