# Sprint 2

## install llama.cpp

### GPU
sudo docker run -d --gpus all -p 8080:8080 --name llm ghcr.io/ggml-org/llama.cpp:server-cuda \
  -hf unsloth/Qwen3.5-4B-GGUF:Q4_K_M --host 0.0.0.0 --port 8080 -ngl 99 -c 4096

### CPU
sudo docker run -d -p 8080:8080 --name llm ghcr.io/ggml-org/llama.cpp:server \
  -hf unsloth/Qwen3.5-4B-GGUF:Q4_K_M --host 0.0.0.0 --port 8080 -c 4096

sudo docker start llm 

curl http://localhost:8080/health
sudo docker logs -f llm


## model
brew install huggingface-cli
hf download unsloth/Qwen3.5-9B-GGUF Qwen3.5-9B-UD-Q4_K_XL.gguf --local-dir ~/Downloads
llama-server -m ~/Downloads/Qwen3.5-9B-UD-Q4_K_XL.gguf -c 2048 -ctk q8_0 -ctv q8_0 --jinja
llama-server -m ~/Downloads/Qwen3.5-9B-UD-Q4_K_XL.gguf -c 8192 -ctk q8_0 -ctv q8_0 -fa --jinja

