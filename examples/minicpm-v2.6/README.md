# MiniCPM-V 2.6

We are engaged in preparing a PR for the Ollama official repository! For now, you can run MiniCPM-V 2.6 with this fork.
Feel free to raise issues if you meet any problems, and we will reply as soon as possible.

## Install Requirements

- cmake version 3.24 or higher
- go version 1.22 or higher
- gcc version 11.4.0 or higher

## Setup the Code

Prepare both our [llama.cpp](https://github.com/OpenBMB/llama.cpp.git) fork and this Ollama fork.

```bash
git clone -b minicpm-v2.6 https://github.com/OpenBMB/ollama.git
cd ollama/llm
git clone -b minicpmv-main https://github.com/OpenBMB/llama.cpp.git
cd ../
```

## Build

Here we give a MacOS example. See the [developer guide](https://github.com/ollama/ollama/blob/main/docs/development.md) for **more platforms**.

```bash
brew install go cmake gcc
```

Optionally enable debugging and more verbose logging:

```bash
# At build time
export CGO_CFLAGS="-g"

# At runtime
export OLLAMA_DEBUG=1
```

Get the required libraries and build the native LLM code:

```bash
go generate ./...
```

Build ollama:

```bash
go build .
```

Start the server:

```
./ollama serve
```

## Running 

1. Create a file named `Modelfile` following this [example](Modelfile). You may have to change to `FROM` field with your local filepaths.

2. Create the model in Ollama:

```
ollama create minicpm-v2.6 -f examples/minicpm-v2.6/Modelfile
```

3. Run:

```
ollama run minicpm-v2.6
```
