## mistral-unslothify

<img align="right" src="icons/mistral.png" width="60" hspace="10"> 
<img align="right" src="icons/hf.png" width="60" hspace="10"> 
<img align="right" src="icons/unsloth.png" width="150" hspace="10">
<p></p>

Use 🤗huggingface and Unsloth to finetune a Mistral pre-trained model on domain data.

The aim here is to fine-tune the Mistral pre-trained model based on a set of text items that will attune it to perform more effectively on a specific domain. Due to the way that fine-tuning works, the model will not 'memorize' these text items as 'facts', but the model weights will be updated so that it can better generate responses that are aligned with the specific language patterns, terminology, and nuances of the domain. A fine-tuned LLM improves not only in generating text in the fine-tuned style but also in recognizing and discerning nuances of that style. 


Maybe surprisingly, in spite of a model such as for example Mistral 7B having seven billion parameters, the number of domain examples needed to fine-tune it can often be relatively small (see, for example, the widely cited paper on LLMs being ['few-shot learners'](https://arxiv.org/abs/2005.14165)). This is because large models like Mistral have a robust foundation of general language understanding, and the fine-tuning acts more like a focused nudge refining what the model already knows, rather than starting from scratch.

As an example here, we have the file `domain.jsonl` with 500 text items to fine-tune the model for. All examples are about Swedish meatballs, so the model will become specifically tailored to text-based tasks around those.






#### NOTE
This whole thing must be run on GPU. Either on a local machine with Nvidia/Cuda properly installed, on Google Colab with a free GPU runtime (even though they quickly run out), or any other cloud machine where the `!nvcc --version` cell below checks out ✅. Options include `brev.dev` and `vast.ai`.



#### Parameters to adjust to counteract overfitting

- `learning_rate` -- a commonly used rate could be around `0.0002` but the higher the rate the quicker the model may overfit. Lower late learns in a more stable way.
- `weight_decay` -- experiment with the value, for example around `0.1` to `0.5`, to penalise large weights to reduce overfitting.
- `warmup_steps` -- increase it (e.g., `10` or more) to help the model start learning in a more gradual and stable way.
- `per_device_train_batch_size` and `gradient_accumulation_steps` -- multiplying the numbers set for these two = batch size, and larger batch sizes can help with stability.
- `lr_scheduler_type` -- your training dynamics might be helped by choosing a different learning rate scheduler (such as `cosine` or `constant_with_warmup`).
- `num_train_epochs` -- the more epochs, the likelier to overfit, but iterating the last cell above can be a way to gradually fine-tune the model to a desired level.
