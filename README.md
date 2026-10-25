## Final : 60 points
```bash
vllm serve ~/tantan/models/MANGO1.5-Qwen3.5-9B \
  --served-model-name CMKL/MANGO1.5-Qwen3.5-9B --host 0.0.0.0 --port 8000 \
  --max-model-len 40960 --max-num-seqs 128 --max-num-batched-tokens 8192 \
  --long-prefill-token-threshold 2048 --mamba-ssm-cache-dtype bfloat16 \
  --kv-cache-dtype fp8 --attention-backend FLASHINFER \
  --reasoning-parser qwen3 --enable-auto-tool-choice --tool-call-parser qwen3_coder \
  --speculative-config '{"method": "mtp", "num_speculative_tokens": 2}' \
  --enable-force-include-usage --language-model-only
```

# Flags in our serve command
- `--served-model-name`: The model name(s) used in the API. (default: None)
- `--host`: Host name. (default: None)
- `--port`: Port number. (default: 8000)
- `--max-model-len`: Model context length (prompt and output). (default: None)
- `--max-num-seqs`: Maximum number of sequences to be processed in a single iteration. (default: None)
- `--max-num-batched-tokens`: Maximum number of tokens that can be processed in a single iteration. (default: None)
- `--long-prefill-token-threshold`: For chunked prefill, a request is considered long if the prompt is longer than this number of tokens. (default: 0)
- `--mamba-ssm-cache-dtype`: The data type to use for the Mamba cache (ssm state only, conv state will still be controlled by mamba_cache_dtype). (default: auto)
- `--kv-cache-dtype`: Data type for kv cache storage. (default: auto)
- `--attention-backend`: Attention backend to use. (default: None)
- `--reasoning-parser`: Select the reasoning parser depending on the model that you're using.
- `--enable-auto-tool-choice`: Enable auto tool choice for supported models. (default: False)
- `--tool-call-parser`: Select the tool call parser depending on the model that you're using. (default: None)
- `--speculative-config`: Speculative decoding configuration. (default: None)
- `--enable-force-include-usage`: If set to True, including usage on every request. (default: False)
- `--language-model-only`: If True, disables all multimodal inputs by setting all modality limits to 0. (default: False)