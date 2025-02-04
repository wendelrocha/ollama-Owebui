# ollama-Owebui
## Instalar o Ollama e o Opern WebUI para rodar modelos LLM

O Ollama é uma plataforma que permite executar modelos de linguagem de grande escala (LLM) localmente em sua máquina, oferecendo maior controle e privacidade. O Open WebUI é uma interface web de código aberto, auto-hospedada e rica em recursos, projetada para operar modelos de linguagem de grande escala (LLMs) localmente. 

**Pré-requisitos:**

- Distro Linux instalada sob o WSL2 no Windows 11.

Usei a distribuição Ubuntu 24.04.1 LTS, executado sob o WSL2-Linux-Kernel: 5.15.167.4-microsoft-standard-WSL2, no Windows 11 Pro 23H2.
Abaixo segue o passo a passo de instalação e configuração, para executar o Ollama em sistemas operacionais Linux Debian Based.

### Instalando no Linux

**1 - Atualize os pacotes do sistema e instale as depedências necessárias:**

    sudo apt update && sudo apt upgrade -y
  
Este commando atualiza os repositórios e instala as atualizações disponíveis para o sistema operacional. 

    sudo apt install -y curl 
  
Este commando instala as depênncias (pacotes) necessários para instalação do Ollama.   
 
**2 - Baixe e execute o script de instalação do Ollama:**

    curl -fsSL https://ollama.com/install.sh | sh
  
Este comando detectará automaticamente a arquitetura do seu sistema e instalará a versão apropriada do Ollama.

**3 - Verifique a instalação:**

    ollama --version

Este comando exibe a versão do Ollama que acabou de ser instalada. 

## Executando o modelos LLM no Ollama

Para executar modelos LLM no Ollama, você precisa fazer o pull do modelo desejado.

**Rodando o DeepSeek-R1 de 1.5B no Ollama**

**1 - Baixe o modelo DeepSeek-R1:**

    ollama pull deepseek-r1:1.5b
 
Este comando fará o download do modelo especificado para o seu sistema.

**2 – Execute o modelo:**

    ollama run deepseek-r1:1.5b

Este comando executa o modelo DeepSeek-R1 de 14 bilhões de parâmetros.
Isso iniciará uma sessão interativa (CLI) onde você pode inserir prompts e receber respostas do modelo diretamente na console.

## Instalando o Open WebUI

A instalação do Open WebUI pode ser realizada de duas maneiras principais: utilizando o Docker ou através de uma instalação manual. Neste laboratório, utilizei a instalação via Docker. 

### Instalação via Docker

**Pré-requisitos:**

- Docker instalado em seu sistema (Docker Desktop integrado ao WSL2 no Windows).

**Baixe e execute a imagem Docker do Open WebUI:**

    docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main

Este comando baixa a imagem do Open WebUI com suporte integrado ao Ollama e a executa em um contêiner Docker. A aplicação ficará acessível em http://localhost:3000

**Explicação dos parâmetros:**

    -d: Executa o contêiner em segundo plano (modo “detached”).

    --add-host=host.docker.internal:host-gateway: Utiliza a rede do host, permitindo que o contêiner acesse serviços em execução no host diretamente.

    -v open-webui:/app/backend/data: Monta um volume chamado open-webui para persistência de dados.

    -e OLLAMA_BASE_URL=http://127.0.0.1:11434: Define a variável de ambiente OLLAMA_BASE_URL para apontar para o Ollama em execução no host. Pode apontar para outro server. 

    --name open-webui: Nomeia o contêiner como open-webui.

    --restart always: Garante que o contêiner seja reiniciado automaticamente em caso de falha.

    ghcr.io/open-webui/open-webui:main: Especifica a imagem do Open WebUI a ser utilizada.

### Integrando o Open WebUI com o Ollama para executar modelos LLM 

**1 - Baixe o modelo desejado, aqui vou usar o DeepSeek-R1:**

    ollama pull deepseek-r1:1.5b
 
Este comando faz o download do modelo especificado para o seu sistema LLM. Caso já tiver baixado anteriormente, este passo é desnecessário.
 
**2 - Configure o Open WebUI para reconhecer o modelo:**

No Open WebUI, vá até a seção de modelos e adicione o modelo deepseek-r1:1.5b à lista de modelos disponíveis.

**3 – Selecione o modelo e comece a interagir:**

Na interface do Open WebUI, selecione o modelo DeepSeek-R1 e comece a inserir prompts para receber respostas geradas pelo modelo.

Pronto! 

Agora você está equipado para explorar o poder do modelo DeepSeek-R1 utilizando o Open WebUI integrado ao Ollama em seu sistema. 

**Para mais informações e suporte, visite o repositório oficial do Ollama no GitHub.** 

**Para o Open WebUI visite a documentação: docs.openwebui.com.**

