# LoRa-Simple-Implementation

Understanding the Research Paper - [LoRA: Low-Rank Adaptation of Large Language Models](https://arxiv.org/pdf/2106.09685.pdf)

### Optimized a Pretrained **Bloom1b7** Model with LoRA:
![LoRA Bloom Model](https://github.com/user-attachments/assets/ea066bca-21b9-413b-a125-d6ad4f304de9)

The **Bloom3b** model contains about **3 billion parameters**, while the **LoRA implementation** optimizes approximately **2.4 million parameters**. By utilizing LoRA, the trainable parameters are reduced to just **0.082%** of the original model size, yet it maintains a training loss of **2.5** over 100 epochs. Notably, the **weight updates** are stored in a compact file of only **10 MB**. 

For such a large model, this optimization technique enables the use of multiple interchangeable modules, each about 10 MB, without significantly sacrificing performance. This highlights the efficiency and scalability of the approach, drastically reducing computational and storage requirements while preserving model quality.

![LoRA Training Process](https://github.com/user-attachments/assets/64f6c713-28a7-425c-b479-6f627f271959)
![Loss Curve](https://github.com/user-attachments/assets/5a1dcff4-d349-4854-9e6d-43397453a0b7)
![Parameter Reduction](https://github.com/user-attachments/assets/7a2df19b-8d1d-4915-90d7-649cc15d6a3a)

---

## What Happens When You Fine-Tune with LoRA:

### 1. **Base Model Stays the Same**:
LoRA keeps the pre-trained base model frozen during fine-tuning. The base model's parameters, typically very large, remain unchanged.

### 2. **LoRA Adapters Are Small**:
Instead of updating the entire parameter set, LoRA introduces small **low-rank matrices** (LoRA adapters) to capture task-specific fine-tuning. These matrices are significantly smaller compared to the full model.

### 3. **Saving the Fine-Tuned Model**:
- Rather than saving the entire model (which could be massive, e.g., 2GB or more), only the **LoRA adapters**—representing the small changes learned during fine-tuning—are saved.
- This results in a much smaller file since you're not saving the base model again, just the small **LoRA components**.

### 4. **Loading the Model for Inference**:
- For inference, load the pre-trained base model and apply the small LoRA adapter to it.
- This means you don't need to reload the entire model—just the LoRA adapters.
- The process is faster, as only the small file containing the fine-tuned parameters needs to be loaded.

---

### Key Takeaways:
- **Efficient and Scalable**: LoRA dramatically reduces computational and storage requirements without sacrificing model quality.
- **Compact Fine-Tuning**: Only the small changes in parameters are stored, making the process highly efficient for large models.
- **Faster Inference**: Loading just the adapters makes the inference process faster and more manageable.
