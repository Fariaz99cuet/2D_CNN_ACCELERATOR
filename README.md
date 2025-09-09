 ![RTL Synthesis](Images/accelerator.jpg)
---

# CNN Hardware Accelerator for Image Processing

This project implements a **hardware accelerator for Convolutional Neural Networks (CNNs)** using Verilog. The design includes **convolution, quantization, ReLU activation, and pooling** stages, optimized for FPGA or ASIC deployment. It is intended for educational purposes as well as small-scale embedded CNN acceleration.

---

## Overview

Modern CNNs require high computational throughput, especially for tasks like image classification, feature extraction, or object detection. General-purpose processors often struggle to meet the performance requirements for real-time applications. This project presents a **specialized hardware accelerator** designed to efficiently perform core CNN operations.

The accelerator supports:

* **2D Convolutions** with configurable kernel size (`k x k`) and stride (`s`).
* **Quantization** for reducing precision and memory usage.
* **ReLU Activation** for introducing non-linearity.
* **Pooling** (Max, Average, Min) for dimensionality reduction.
* **Pipeline registers** to maintain data flow and synchronization.
* **Optional parallel MAC units (`NUM_MAC`)** to increase throughput.

---

## Features

1. **Convolution Module (`convolver`)**

   * Implements a 2D sliding window for convolution.
   * Supports configurable input size, kernel size, stride, and bit precision.
   * Parallelizable using `NUM_MAC` units for faster multiply-accumulate operations.

   **Example:**
   ![Sliding Window Example](images/sliding_window.png)
   *Illustration of the 3×3 convolution sliding over a 6×6 input.*

2. **Quantizer Module (`quantizer`)**

   * Reduces bit width while maintaining significant data.
   * Truncates lower precision bits to save memory and hardware resources.

   **Example:**
   ![Quantization Example](images/quantization.png)
   *Input data reduced from 16-bit to 12-bit fractional precision.*

3. **ReLU Module (`relu`)**

   * Applies the Rectified Linear Unit function: outputs zero for negative inputs and passes positive values unchanged.

   **Example:**
   ![ReLU Activation](images/relu.png)

4. **Pooling Module (`pooler`)**

   * Supports max, average, and min pooling.
   * Reduces feature map dimensions to save memory and computation.

   **Example:**
   ![Pooling Operation](images/pooling.png)

5. **Pipeline Architecture**

   * Registers between each stage (convolution → quantization → ReLU → pooling) ensure smooth data flow.
   * Enables potential throughput improvement in larger designs.

6. **Testbench & Verification**

   * Includes a fully functional testbench with pseudo-random test vectors.
   * Displays intermediate signals for debugging convolution operations.

---

## Design Parameters

| Parameter | Description                                                 |
| --------- | ----------------------------------------------------------- |
| `N`       | Bit width for data (default 16)                             |
| `Q`       | Fractional bits for fixed-point representation (default 12) |
| `n`       | Input image size (default 6x6)                              |
| `k`       | Convolution kernel size (default 3x3)                       |
| `p`       | Pooling window size (default 2x2)                           |
| `s`       | Stride for convolution (default 1)                          |
| `NUM_MAC` | Number of parallel MAC units for convolution (default 4)    |

---

## Usage

1. **Clone the repository**

```bash
git clone https://github.com/your-username/cnn-hardware-accelerator.git
cd cnn-hardware-accelerator
```

2. **Simulate the design** using your preferred Verilog simulator (e.g., ModelSim, Vivado, Icarus Verilog).
3. **Modify parameters** like `n`, `k`, or `NUM_MAC` for different CNN configurations.
4. **Add custom test vectors** for real CNN images.

---

## Future Work

* Support for **multi-channel convolutions** (3D CNNs).
* Integration with **FPGA boards** for real-time image processing.
* Optimization for **higher bit-width quantization** and dynamic precision.
* **Pipeline parallelization** using multiple `NUM_MAC` units for higher throughput.

---



