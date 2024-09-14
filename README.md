<h1 align="center">🛠️ FluxForge</h1>

<p align="center">
  <i>Effortless AI Tool Deployment and Guides for Flux1.0, Ollama, and Beyond</i>
</p>

<p align="center">
  <a href="https://github.com/diogocgi/fluxforge/graphs/contributors">
    <img alt="Contributors" src="https://img.shields.io/github/contributors/diogocgi/fluxforge?style=flat-square">
  </a>
  <a href="https://github.com/diogocgi/fluxforge/network/members">
    <img alt="Forks" src="https://img.shields.io/github/forks/diogocgi/fluxforge?style=flat-square">
  </a>
  <a href="https://github.com/diogocgi/fluxforge/stargazers">
    <img alt="Stars" src="https://img.shields.io/github/stars/diogocgi/fluxforge?style=flat-square">
  </a>
  <a href="https://github.com/diogocgi/fluxforge/issues">
    <img alt="Issues" src="https://img.shields.io/github/issues/diogocgi/fluxforge?style=flat-square">
  </a>
  <a href="https://github.com/diogocgi/fluxforge/pulse">
    <img alt="Commit Activity" src="https://img.shields.io/github/commit-activity/m/diogocgi/fluxforge?style=flat-square">
  </a>
  <a href="https://github.com/diogocgi/fluxforge/blob/main/LICENSE">
    <img alt="License" src="https://img.shields.io/github/license/diogocgi/fluxforge?style=flat-square">
  </a>
</p>

## Introduction

With the release of [Flux1.0](https://github.com/black-forest-labs/flux) by **Black Forest Labs** I regained my interest with image generation and started exploring how to train Lora's for Flux.

From my research, there is a lot of information in the web regarding dataset generation and training for Flux and other image generation models, but it is scatttered throughout numerous Reddit posts, GitHub issues, websites, etc.

Setting up the development environment is also a hassle, even more so for people without much programming knowledge, which may lead to many giving up before even starting.

To tackle both these issues, I created this repository to serve as a spot for enabling people to easely deploy containarized tools and guides for various Machine Learning related tasks.

🎉 Let's make model training easily accessible! 🎉

## Main tools setup

### 0. Prerequisites

Make sure you have **docker** and **docker compose** correctly setup on you pc.

Follow the instructions at Docker's official documentation, mainly:
- 1.1 [Uninstall old versions](https://docs.docker.com/engine/install/ubuntu/#uninstall-old-versions)
- 1.2 [Install using the apt repository](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)

### 1. Ollama + WebUI + Search

> Make sure you don't have Ollama locally installed, otherwise the dockerized Ollama won't be able to start due to the 11434 port being in use

Each service will be available at:
- WebUI: http://127.0.0.1:8081
- Ollama: http://127.0.0.1:11434
- SearcXng: http://127.0.0.1:11435

```bash
docker-compose -f ./dockercompose/docker-compose.ollama.yaml up -d

# check health status of the services
docker ps -a

# download llama3.1 through the dockerized ollama
docker exec -it ollama ollama pull llama3.1
docker exec -it ollama ollama list
```

Go to http://127.0.0.1:8080/ and check if:
- you are able to select the downloaded Llama3.1 model
- you can toggle the web search in the plus button on the left side of the prompt textfield

#### Allow WebUI to search with searxng

To allow WebUI to successfully query searxng for results, you need to make sure that you have `json` in the list of formats in searxng `settings.yml` file:

```yml
# dockercompose/searxng/settings.yml
...

  # remove format to deny access, use lower case.
  # formats: [html, csv, json, rss]
  formats:
    - html
    - json

...
```

## On the horizon...

- [x] Containarized Ollama + Webui + Search
- [ ] Containarized ComfyUI
- [ ] Containarized Flux1.0 Dev Lora training with [sd-scripts](https://github.com/kohya-ss/sd-scripts)
- [ ] ComfyUI Workflows for basic Flux usage
- [ ] ComfyUI Workflows for dataset generation
- [ ] ComfyUI Workflows for dataset captioning
- [ ] Lora dataset generation guides
- [ ] Flux Lora training guides


## Contributions

Feel free to contribute! I'm far from an expert but I'll do my best to keep up 🍻!


## Resources

- https://github.com/kohya-ss/sd-scripts
- https://github.com/comfyanonymous/ComfyUI
- https://github.com/ollama/ollama
- https://github.com/open-webui/open-webui
