<div align="center">

<img style="width:250px; height: 90px " src="https://cis.ieee.org/images/files/Branding/logos/white/IEEE_CIS_logo_White_RGB_300ppi.png" />

# Sign App

[![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)](https://github.com/seu-usuario/sign-app)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](https://claude.ai/chat/LICENSE)
[![React Native](https://img.shields.io/badge/React%20Native-0.73-61DAFB.svg?logo=react)](https://reactnative.dev/)
[![Node](https://img.shields.io/badge/Node-22.0-339933.svg?logo=node.js)](https://nodejs.org/)

</div>

Bem-vindo ao Sign-App\! Este documento irá guiá-lo através do processo de configuração do ambiente e execução do projeto de forma 100% automatizada. O objetivo é que você precise de apenas **um comando** para ter o ambiente de desenvolvimento rodando.


### Sumário

  * [Pré-requisitos](https://www.google.com/search?q=%23%EF%B8%8F-pr%C3%A9-requisitos)
  * [Como Rodar o Projeto](https://www.google.com/search?q=%23%EF%B8%8F-como-rodar-o-projeto)
  * [O que o Script de Automação Faz?](https://www.google.com/search?q=%23-o-que-o-script-de-automa%C3%A7%C3%A3o-faz)
  * [Solução de Problemas (Troubleshooting)](https://www.google.com/search?q=%23-solu%C3%A7%C3%A3o-de-problemas-troubleshooting)

### Pré-requisitos

Antes de começar, certifique-se de que você tem as seguintes ferramentas instaladas e configuradas em sua máquina:

  * [**Git**](https://git-scm.com/downloads)
  * [**Node.js e NPM**](https://nodejs.org/)
  * [**Docker e Docker Compose**](https://www.docker.com/products/docker-desktop/)
  * [**Android SDK Command-Line Tools**](https://developer.android.com/studio) 
  * **Pelo menos um Emulador (AVD)** Você precisa ter um Android Virtual Device criado.

**IMPORTANTE:** Após instalar o Android SDK, é necessário configurar a variável de ambiente `ANDROID_HOME` apontando para o diretório do SDK. 



### ▶️ Como Rodar o Projeto

Com o ambiente devidamente configurado,

#### Passo 1: Clone o Repositório

```bash
git clone https://github.com/seu-usuario/seu-repositorio.git
cd seu-repositorio
```

#### Passo 2: Execute o Script de Automação

Escolha o comando correspondente ao seu sistema operacional. O comando cobrirá desde a instalação de dependências dentro do Docker até a inicialização do app.

##### 🐧 Para Linux ou macOS:

```bash
npm run dev:start:unix
```

##### 💻 Para Windows (usando CMD ou PowerShell):

```bash
npm run dev:start:win
```

E pronto, suas alterações no código serão refletidas automaticamente no emulador (Hot Reload).

### Dentro dos entrypoints 

O comando `npm run dev:start:*` executa uma série de passos para criar um ambiente de desenvolvimento completo e funcional:

 - 1 Verifica se a variável de ambiente `ANDROID_HOME` está configurada.
 - 2 Encontra um emulador Android (AVD) disponível em sua máquina.
 - 3 Inicia o emulador automaticamente em segundo plano.
 - 4 Aguarda o sistema operacional do emulador carregar por completo.
 - 5 Inicia o container Docker (via `docker-compose`), que irá:

  - Construir a imagem, executando `npm install` **dentro do container**.
  - Iniciar o servidor Metro Bundler.
    🔗 Configura o `adb reverse`, permitindo que o app no emulador se comunique com o Metro dentro do container.
    📲 Instala e inicia o aplicativo React Native no emulador.

### Solução de Problemas (Troubleshooting)

1.  **Erro: `A variável de ambiente ANDROID_HOME não está definida.`**

      * **Solução:** Você precisa criar a variável de ambiente `ANDROID_HOME` e fazê-la apontar para a pasta onde seu Android SDK foi instalado.

2.  **Erro: `Nenhum emulador (AVD) encontrado.`**

      * **Solução:** Você precisa criar um dispositivo virtual através do AVD Manager no Android Studio ou via linha de comando com `avdmanager`.

3.  **O Docker parece não funcionar ou o comando `docker-compose` falha.**

      * **Solução:** Certifique-se de que o Docker Desktop está em execução na sua máquina.

4.  **O comando `adb` não foi encontrado.**

      * **Solução:** O `adb` fica na pasta `platform-tools` dentro do seu Android SDK. Adicione `%ANDROID_HOME%\platform-tools` (Windows) ou `$ANDROID_HOME/platform-tools` (Linux/macOS) à sua variável de ambiente `PATH`.

5.  **Erro durante o `docker-compose up` (falha no `npm install` dentro do container).**

      * **Solução:** Isso pode ser um problema de rede ou um pacote quebrado no `package.json`. Tente forçar uma reconstrução limpa da imagem com o comando: `docker-compose build --no-cache` e depois rode o script de start novamente. Verifique o log do Docker para mensagens de erro específicas do `npm`.
