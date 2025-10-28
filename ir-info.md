# 🧠 Intermediate Representation (IR) Specification

This document outlines the structure and metadata stored in the **Intermediate Representation (IR)** designed for encrypted neural network inference.  
The IR serves as a **backend-agnostic layer** between high-level models (e.g., ONNX) and low-level homomorphic encryption backends (CKKS, TFHE).

---

## 1. Overview

The IR captures both **structural** and **semantic** information of a model while remaining independent of any specific framework or encryption scheme.  
Its main goals are:

- To standardize tensor and operation metadata for analysis and transformation.  
- To enable lowering to multiple encrypted inference backends.  
- To preserve all necessary information for graph-level optimization, scheduling, and packing.

---

## 2. Core Components

### 2.1 IR Graph

The IR graph is a **directed acyclic graph (DAG)** representing computation flow.  
Each node corresponds to an operation, and edges represent tensors flowing between operations.

| Field | Description |
|--------|--------------|
| **id** | Unique identifier of the operation node. |
| **op_type** | Operation type (e.g. `Conv2D`, `MatMul`, `ReLU`, `Add`). |
| **inputs** | List of input tensor references. |
| **outputs** | List of output tensor references. |
| **attributes** | Operation-specific attributes (e.g. strides, kernel size, padding). |
| **backend_flags** | Backend hints (e.g. packing scheme, scaling strategy, ciphertext modulus level). |
| **location_info** *(optional)* | Source location from frontend graph (for debugging or visualization). |

---

### 2.2 Tensor Metadata

Each tensor in the IR is represented as a **typed value** carrying structural and type information.

| Field | Description |
|--------|--------------|
| **name** | Tensor identifier |
| **shape** | List of dimensions. Would probably be static (`[1,3,224,224]`) |
| **dtype** | Element data type (e.g. `float32`, `int64`). |
| **layout** | Memory or channel layout (e.g. `NCHW`, `NHWC`). |
| **range_estimation** | chosing scale parameters for ckks, determining quantization bit-width for tfhe |
| **quantization_info** *(optional)* | Scale, zero-point, bitwidth for quantized models. |
| **encryption_info** *(optional)* | Ciphertext slot count, packing format, noise budget level. |
| **producer / consumers** | References to source and destination operation nodes. |

---



### 2.3 Activation Functions Metadata -- ?

---

### 2.4 Model Metadata

Global information about the model and compilation context.

| Field | Description |
|--------|--------------|
| **model_name** | Original model name or file. |
| **framework_origin** | Source framework (e.g. `onnx`, `torch`, `tensorflow`). |
| **version** | IR or frontend version used during import. |
| **input_tensors** | List of entry tensor definitions (with shape and type). |
| **output_tensors** | List of exit tensor definitions. |
| **target_backend** | Desired backend (`CKKS`, `TFHE`, or `Plaintext`). |
| **normalization_parameters** |  |
| **preprocessing_information** |  |



---

## 4. Example Representation

Example snippet (JSON-like form):

```json
{
  "model_name": "ResNet18",
  "target_backend": "CKKS",
  "inputs": [
    { "name": "input", "shape": [1, 3, 224, 224], "dtype": "float32" }
  ],
  "nodes": [
    {
      "id": "conv_1",
      "op_type": "Conv2D",
      "inputs": ["input", "conv1_weight", "conv1_bias"],
      "outputs": ["conv1_out"],
      "attributes": {
        "kernel_shape": [7, 7],
        "strides": [2, 2],
        "pads": [3, 3, 3, 3]
      }
    },
    {
      "id": "relu_1",
      "op_type": "ReLU",
      "inputs": ["conv1_out"],
      "outputs": ["relu1_out"]
    }
  ]
}
