## mistral-unslothify

Use 🤗huggingface and Unsloth to finetune a Mistral pre-trained model on domain data.

The aim here is to fine-tune the Mistral pre-trained model based on a set of text items that will attune it to perform more effectively on a specific domain. This means that we will be adapting the general capabilities of the model to better suit the needs and nuances of a particular field or area of expertise.

Maybe surprisingly, in spite of a model such as for example Mistral 7B having seven billion parameters, the number of domain examples needed to fine-tune it can often be relatively small (see, for example, the widely cited paper on LLMs being ['few-shot learners'](https://arxiv.org/abs/2005.14165)). This is because large models like Mistral have a robust foundation of general language understanding, and the fine-tuning acts more like a focused nudge refining what the model already knows, rather than starting from scratch.

As an example here, we have the file `domain.jsonl` with 500 text items to fine-tune the model for. All examples are about burgers 🍔🍔🍔, so the model will become specifically tailored to text-based tasks around burgers.

<img align="right" src="icons/mistral.png" width="60" hspace="10"> 
<img align="right" src="icons/hf.png" width="60" hspace="10"> 
<img align="right" src="icons/unsloth.png" width="150" hspace="10">

<hr>
**NOTE**<br>
This whole thing must be run on GPU. Either on a local machine with Nvidia/Cuda properly installed, on Google Colab with a free GPU runtime (even though they quickly run out), or any other cloud machine where the `!nvcc --version` cell below checks out ✅. Options include `brev.dev` and `vast.ai`.