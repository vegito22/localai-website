
+++
disableToc = false
title = "🦙 llama.cpp"
weight = 1
+++

[llama.cpp](https://github.com/ggerganov/llama.cpp) is a popular port of Facebook's LLaMA model in C/C++.

## Features

The `llama.cpp` model supports the following features:
- [📖 Text generation (GPT)]({{%relref "features/text-generation" %}})
- [🧠 Embeddings]({{%relref "features/embeddings" %}})
- [🔥 OpenAI functions]({{%relref "features/openai-functions" %}})
- [✍️ Constrained grammars]({{%relref "features/constrained_grammars" %}})

## Setup

LocalAI supports `llama.cpp` models out of the box. You can use the `llama.cpp` model in the same way as any other model. 

### Manual setup

It is sufficient to copy the `ggml` model files in the `models` folder. You can refer to the model in the `model` parameter in the API calls.

[You can optionally create an associated YAML]({{%relref "advanced" %}}) model config file to tune the model's parameters or apply a template to the prompt.

Prompt templates are useful for models that are fine-tuned towards a specific prompt. 

### Automatic setup

LocalAI supports model galleries which are indexes of models. For instance, the huggingface gallery contains a large curated index of models from the huggingface model hub for `ggml` models.

For instance, if you have the galleries enabled, you can just start chatting with models in huggingface by running:

```bash
curl http://localhost:8080/v1/chat/completions -H "Content-Type: application/json" -d '{
     "model": "TheBloke/WizardLM-13B-V1.2-GGML/wizardlm-13b-v1.2.ggmlv3.q2_K.bin",
     "messages": [{"role": "user", "content": "Say this is a test!"}],
     "temperature": 0.1
   }'
```

LocalAI will automatically download and configure the model in the `model` directory.

Models can be also preloaded or downloaded on demand. To learn about model galleries, check out the [model gallery documentation]({{%relref "models" %}}).

### YAML configuration

To use the `llama.cpp` backend, specify