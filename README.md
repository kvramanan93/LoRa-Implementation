# LoRa-Simple-Implementation
Understanding the Research paper - LoRA : https://arxiv.org/pdf/2106.09685.pdf
Optimized a pretrained bloom1b7 model with lora:
![{D61B2437-6024-4A77-A81F-08EC8AFCD91D}](https://github.com/user-attachments/assets/ea066bca-21b9-413b-a125-d6ad4f304de9)
**Bloom3b** model has about **3 billion parameters** and **LoRA implementation** has worked on about **2.4 million parameters** 
The trainable parameters in this implementation are reduced to approximately **0.082%** of the original model size, while 
maintaining a training loss of 2.5 over 100 epochs. Remarkably, the **weight updates are stored** in a compact file of about 
**10 MB**. For such a large model, this optimization technique allows for multiple interchangeable modules, each around
10 MB, delivering similar performance. This highlights the efficiency and scalability of the approach, significantly 
reducing computational and storage requirements without compromising model quality.

![{8DB43899-54A6-4637-BD6E-C0202FE7BF06}](https://github.com/user-attachments/assets/64f6c713-28a7-425c-b479-6f627f271959)
![{747A5C8E-961B-41C3-8478-A38A7B796797}](https://github.com/user-attachments/assets/5a1dcff4-d349-4854-9e6d-43397453a0b7)
![{73C427B2-F73A-498F-AE98-846D5FA9F535}](https://github.com/user-attachments/assets/7a2df19b-8d1d-4915-90d7-649cc15d6a3a)


What Happens When You Fine-Tune with LoRA:
1. Base Model Stays the Same:
LoRA keeps the pre-trained base model frozen during fine-tuning. It doesn't modify the base model's parameters, which are
typically very large.

2. LoRA Adapters Are Small:
* Instead of updating the entire set of parameters, LoRA introduces small low-rank matrices (LoRA adapters) to capture the 
task-specific fine-tuning. These matrices are much smaller in size compared to the full model.

3.When You Save the Fine-Tuned Model:
* Instead of saving the entire model (which might be huge, e.g., 2GB or more), you can just save the LoRA adapters, which 
represent the small changes that were learned during fine-tuning.
* This results in a much smaller file because you're not saving the base model again, just the tiny LoRA components.

4. Loading the Model for Inference:
* When you want to use this fine-tuned model, you can load the pre-trained base model (which you already have) and then 
apply the small LoRA adapter to it.

This means:
* You dont need to reload the entire model, just the LoRA adapters.
* This makes the loading process faster, as youre only loading and applying a small file containing the fine-tuned parameters.
