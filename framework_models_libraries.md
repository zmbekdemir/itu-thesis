# 🔐 Encrypted Deep Learning: Models, Frameworks, and Libraries

This document outlines the models, frameworks, and homomorphic encryption libraries considered in my research comparing **CKKS** and **TFHE** schemes for encrypted inference.

---

## ⚙️ Frameworks and HE Libraries

| Framework/Compiler/Tool/Library    | HE Scheme | Backend Library     | Related Articles | Notes |
|--------------|-----------|---------------------|------------------|-------|
| **ANT-ACE**  | CKKS      | Custom RNS-CKKS backend | [1](#article-1) | Advanced compiler ecosystem for FHE. Accepts a pretrained ONNX model as input and directly generates C/C++ programs to perform NN inference. Mentions a comparison between FHE compilers: E3, nGraph-HE, CHET, EVA, Transpiler, HECO, Fhelipe|
| **Intel HE-Transformer for nGraph** | CKKS | SEAL | [2](#article-2) | (!NO LONGER SUPPORTED!) HE-Transformer uses a client-aided protocol in which the server sends the encrypted data to the client, which decrypts the data, performs the operation, encrypts the output, and sends it back to the server.
| **CHET**     | CKKS      | Microsoft SEAL      | [3](#article-3)  | (!NOT OPEN SOURCE)Compiler for encrypted tensor programs |
| **HELib**     | CKKS/BGV      | This is a library [Github](https://github.com/homenc/HElib)     | [4](#article-4), [10](#article-10)  | HElib is an open-source software library that implements homomorphic encryption. It supports the BGV scheme with bootstrapping and the Approximate Number CKKS scheme. |
| **Concrete-ML/Zama** | TFHE | This is a library [Github](https://github.com/zama-ai/concrete-ml)  | [6](#article-6), [10](#article-10) | Concrete ML: Privacy Preserving ML framework using Fully Homomorphic Encryption (FHE), built on top of Concrete, with bindings to traditional ML frameworks.
| **SEALion** |   CKKS         | SEAL |  [7](#article-7)|
| **SEAL** | CKKS | This is a library [Github](https://github.com/microsoft/SEAL) | [2](#article-2), [3](#article-3), [5](#article-5), [7](#article-7), [10](#article-10), [13](#article-13)
| **Lattigo** |  CKKS   | This is a library [Github](https://github.com/tuneinsight/lattigo)| [8](#article-8), [11](#article-11) |
| **TenSEAL**  | CKKS      | Microsoft SEAL      | [5](#article-5), [10](#article-10)  | Encrypted PyTorch inference |
| **HEaaN** | ?
| **Concrete** | TFHE      | Zama's TFHE backend | [6](#article-6), [10](#article-10) | High-level TFHE framework |

---

## 🧠 Neural Network Models

| Model Name     | Task                  | Dataset   | Related Articles | Notes                      |
|----------------|-----------------------|-----------|------------------|----------------------------|
| ResNet-20      | Image classification  | CIFAR-10  | [1](#article-1) |   |
| ResNet-32      | Image classification  | CIFAR-10  | [1](#article-1) | 
| ResNet-44      | Image classification  | CIFAR-10  | [1](#article-1) | 
| ResNet-56      | Image classification  | CIFAR-10  | [1](#article-1) | 
| ResNet-110     | Image classification  | CIFAR-10  | [1](#article-1) | 
| MobileNetV2    |                       |           | [2](#article-2) | Mentioned that can be found from tensorflow |
| ResNet-50      | Image classification  |           | [2](#article-2) |


---

## 📚 Articles and References

### 1. ANT-ACE: An FHE Compiler Framework for Automating Neural Network Inference  
[GitHub](https://github.com/ant-research/ace-compiler) | [Paper](https://dl.acm.org/doi/pdf/10.1145/3696443.3708924)  
A production-quality, open-source FHE compiler design. ANT-ACE is a compiler infrastructure that fully automates
neural network inference on encrypted data using FHE, providing a robust open-source platform. It transforms ONNX
inference models into C/C++ programs with its custom opensource FHE library. Designed with a versatile compiler infrastructure supporting multiple levels of abstraction, ANT-ACE
aims to support various input formats and computer architectures across different FHE schemes. Currently, it operates
with the RNS-CKKS scheme on CPU platforms.

### 2. Enabling Homomorphically Encrypted Inference for Large DNN Models  
[Paper](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9417740)
In this work, they present, an exhaustive performance analysis of an HE framework running on a system with hybrid DRAM + persistent
memory subsystems. In summary, the contributions of this article are: (1) They
report the largest DNN models run to date using HE; (2)
They report for the first time the use of persistent memory
technology to enable large DNN inference leveraging HE;
and (3) They provide the corresponding novel in-depth analysis of the viability of using persistent memory technologies
for this specific use case.

### 3. CHET: An Optimizing Compiler for Fully-Homomorphic Neural-Network Inferencing  
[Paper](https://dl.acm.org/doi/pdf/10.1145/3314221.3314628)  
Compiler for encrypted tensor programs.
(!NOT OPEN SOURCE)

### 4. CryptoDL: Deep Neural Networks over Encrypted Data  
[Paper](https://arxiv.org/pdf/1711.05189)
"The main contributions of this work are as follows.
• We provide theoretical foundation to prove that it is possible to find lowest degree polynomial
approximation of a function within a certain error range.
• Building upon the theoretical foundation, we investigate several methods for approximating
commonly used activation functions in CNNs (i.e. ReLU, Sigmoid, and Tanh) with low-degree
polynomials to find the best approximation.
• We utilize these polynomials in CNNs and analyze the performance of the modified algorithms.
• We implement the CNNs with polynomial approximations as activation functions over encrypted
data and report the results for two of the widely used datasets in deep learning, MNIST and
CIFAR-10.
• Our experimental results of MNIST show that CryptoDL can achieve 99.52% accuracy which
is very close to the original model’s accuracy of 99.56%. Also, it can make close to 164000
predictions per hour. These results show that CryptoDL provides efficient, accurate, and
scalable privacy-preserving predictions."

### 5. nGraph-HE2: A High-Throughput Framework for Neural Network Inference on Encrypted Data  
[Paper](https://arxiv.org/pdf/1908.04172)
(!CAN NOT FIND)

### 6. Deep Neural Networks for Encrypted Inference with TFHE  
[Paper](https://arxiv.org/pdf/2302.10906)
"In this work we show how to build neural networks that are FHE compatible,
while minimizing the cryptography knowledge needed by the machine learning
practitioner. We based our work on the Concrete Library [7] which uses TFHE
[6], works over integers, provides a fast programmable bootstrapping mechanism,
and performs exact computation.
"

### 7. SEALion: a Framework for Neural Network Inference on Encrypted Data  
[Paper](https://arxiv.org/pdf/1904.12840)
(!NOT OPEN SOURCE)
"In this paper, we introduce SEALion, a new framework for
implementing machine learning algorithms that can operate
on homomorphically encrypted data and generate encrypted
predictions."

### 8. Parallel Secure Inference for Multiple Models Based on CKKS  
[Paper](https://link.springer.com/chapter/10.1007/978-981-97-7241-4_13)
The main
goal of this paper is to improve the batch processing capability of CKKS to
reduce the number of ciphertexts and computational operations. To achieve this
goal, we suggest increasing the amount of content within a single ciphertext and
parallelizing the computation. 

### 9. A Fast and Accurate Non-interactive Privacy-Preserving Neural Network Inference Framework  
[Paper](https://link.springer.com/chapter/10.1007/978-3-031-51399-2_9)
 Specifically, we utilize
CKKS encryption to enable private neural network inference under floating-point
arithmetic. Leveraging the characteristics of both wordwise HE and bitwise HE,
we design a non-interactive and fast matrix multiplication scheme, achieving up
to 500× acceleration across different matrix dimensions. By transforming various
types of homomorphic encryption ciphertexts and employing lookup tables, we
realize accurate computation of arbitrary non-linear operations without requiring
interaction

### 10. Improving Inference Privacy for Large Language Models using Fully Homomorphic Encryption  
[Paper](https://www2.eecs.berkeley.edu/Pubs/TechRpts/2024/EECS-2024-225.pdf)
The goal of this project is to design a system where the threat actor is not able to glean any
private information from the user. Private information includes the input contents and the
output. This means that any information sent to the server cannot be used by the server
to derive this information. This will be done by only sending the server FHE ciphertexts of
information that could be used to derive the input, intermediate products, or the output.
However, it is not a goal of the project to protect the pre-trained weights or information
about the model protocol itself, as these are considered to be public information known to all
parties. Additionally, it is not a goal for the protocol to guarantee correctness or availability
when it is under attack. As such, a threat actor is allowed to corrupt the model outputs or
deny service to the user as long as this does not lead to the disclosure of private information.
It is also not a goal of the project to hide potentially sensitive information unrelated to the
inference itself, such the IP address of the client or the frequency of requests. The length of
the input itself is also not protected by the system.


### 11. Optimized Privacy-Preserving CNN Inference With Fully Homomorphic Encryption  
[Paper](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=10089847)
[Github](https://github.com/dwkim606/optimal_conv)

### 12. A Secure Convolutional Neural Network Inference Model Based on Homomorphic Encryption  
[Paper](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=10541346) ?

### 13. CryptoNets: Applying Neural Networks to Encrypted Data with High Throughput and Accuracy  
[Paper](https://proceedings.mlr.press/v48/gilad-bachrach16.pdf)

---

## ✅ To Do

- [ ] ?
