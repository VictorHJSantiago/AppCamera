<div align="center">

<img src="https://cdn-icons-png.flaticon.com/512/685/685655.png" alt="AppCamera Logo" width="110" />

# 📸 AppCamera — Aplicativo Android

**Um aplicativo Android nativo, desenvolvido em Java, que demonstra como acionar**
**a câmera do dispositivo para tirar fotos e gravar vídeos via Android Intents.**

<br>

![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Android](https://img.shields.io/badge/Android-3DDC84?style=for-the-badge&logo=android&logoColor=white)
![Gradle](https://img.shields.io/badge/Gradle-02303A?style=for-the-badge&logo=gradle&logoColor=white)
![MediaStore](https://img.shields.io/badge/API-MediaStore-blueviolet?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completo_(Demo)-brightgreen?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)

</div>

---

## 📚 Tabela de Conteúdos

> Navegue rapidamente pelas seções do projeto.

| # | Seção |
|:-:|:------|
| 1 | [📖 Sobre o Projeto](#-sobre-o-projeto) |
| 2 | [✨ Funcionalidades Principais](#-funcionalidades-principais) |
| 3 | [🛠️ Pilha de Tecnologias](#️-pilha-de-tecnologias) |
| 4 | [🔑 Destaques da Implementação](#-destaques-da-implementação) |
| 5 | [📂 Estrutura do Repositório](#-estrutura-do-repositório) |
| 6 | [🚀 Como Executar](#-como-executar) |
| 7 | [🤝 Como Contribuir](#-como-contribuir) |
| 8 | [👨‍💻 Autor](#-autor) |
| 9 | [📄 Licença](#-licença) |

---

## 📖 Sobre o Projeto

> **AppCamera** é um projeto de demonstração Android que ilustra uma das funcionalidades mais comuns do ecossistema mobile: **interagir com a câmera do dispositivo** de forma simples, segura e sem complexidade desnecessária.

Em vez de construir uma interface de câmera do zero (usando APIs de baixo nível como `CameraX` ou `Camera2`), este app utiliza **Android Intents via `MediaStore`** — a abordagem recomendada para delegar o pedido à câmera nativa do dispositivo, aproveitando toda a sua estabilidade e compatibilidade.

Após a captura, o vídeo gravado é recebido pelo `onActivityResult` e reproduzido diretamente em um `VideoView` na tela principal.

---

## ✨ Funcionalidades Principais

| Ícone | Funcionalidade | Intent Utilizada | Descrição |
|:-----:|:---------------|:----------------:|:----------|
| 📸 | **Tirar Foto** | `ACTION_IMAGE_CAPTURE` | Abre a câmera nativa do dispositivo no modo fotografia. |
| 📹 | **Gravar Vídeo** | `ACTION_VIDEO_CAPTURE` | Abre a câmera nativa no modo de gravação de vídeo. |
| 📺 | **Reprodução de Vídeo** | `onActivityResult` | Captura o retorno da gravação e reproduz automaticamente no `VideoView`. |
| 🎨 | **Design Personalizado** | — | Fundo em gradiente (`bg_gradient.xml`) e ícones vetoriais (`ic_camera.xml`, `ic_videocam.xml`). |

> ⚠️ **Nota de Implementação:** Na versão atual, o app está preparado para lidar com o retorno do vídeo. A captura do `Bitmap` retornado pela foto via `onActivityResult` ainda não está implementada.

---

## 🛠️ Pilha de Tecnologias

| Tecnologia | Função no Projeto |
|:-----------|:------------------|
| **Java** | Linguagem principal de toda a lógica do aplicativo. |
| **Android SDK** | Framework nativo para desenvolvimento Android. |
| **XML (Layouts)** | Define a interface do usuário: botões, `VideoView` e estrutura visual. |
| **Android Intents (MediaStore)** | `ACTION_IMAGE_CAPTURE` e `ACTION_VIDEO_CAPTURE` para delegar à câmera nativa. |
| **VideoView** | Componente nativo para reprodução do vídeo capturado diretamente na tela. |
| **AndroidManifest.xml** | Declaração de permissões e features de hardware necessárias. |
| **Gradle (Kotlin DSL)** | Sistema de build e gestão de dependências do projeto. |

### 🔐 Permissões Declaradas

| Permissão | Finalidade |
|:----------|:-----------|
| `android.permission.CAMERA` | Acesso à câmera do dispositivo. |
| `android.permission.RECORD_AUDIO` | Captura de áudio durante a gravação de vídeo. |
| `android.hardware.camera` | Feature de hardware — indica que o app requer câmera. |

---

## 🔑 Destaques da Implementação

### 📷 Fluxo via Android Intents

> A abordagem com Intents é a forma mais simples, segura e compatível de usar a câmera no Android — sem a complexidade de gerenciar permissões de câmera em tempo de execução ou ciclo de vida do preview.

```java
// Exemplo: Acionar a câmera para gravar vídeo
Intent intent = new Intent(MediaStore.ACTION_VIDEO_CAPTURE);
startActivityForResult(intent, REQUEST_CODE_VIDEO);

// Receber o vídeo gravado de volta
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);

    if (requestCode == REQUEST_CODE_VIDEO && resultCode == RESULT_OK) {
        Uri videoUri = data.getData();    // URI do vídeo gravado
        videoView.setVideoURI(videoUri);  // Carrega no VideoView
        videoView.start();               // Reproduz automaticamente
    }
}
```

**Fluxo resumido:**

```
👆 Usuário pressiona "Gravar Vídeo"
          ↓
📤 startActivityForResult() dispara a Intent
          ↓
📹 Câmera nativa do dispositivo abre
          ↓
✅ Usuário finaliza a gravação
          ↓
📥 onActivityResult() recebe o resultado
          ↓
📺 VideoView carrega e reproduz o vídeo
```

---

## 📂 Estrutura do Repositório

```plaintext
appcamera/
│
├── 📄 build.gradle.kts                    # ⚙️  Configurações do projeto (nível raiz)
├── 📄 settings.gradle.kts                 # ⚙️  Configurações do Gradle
│
└── 📁 app/
    ├── 📄 build.gradle.kts                # ⚙️  Configurações do módulo 'app'
    │
    └── 📁 src/main/
        │
        ├── 📄 AndroidManifest.xml         # 🔐 Permissões, features e atividades
        │
        ├── 📁 java/com/example/appcamera/
        │   └── 📄 MainActivity.java       # 🧠 Lógica principal — Intents e VideoView ← CORE
        │
        └── 📁 res/
            ├── 📁 layout/
            │   └── 📄 activity_main.xml   # 🖼️  Interface do usuário (botões + VideoView)
            └── 📁 drawable/
                ├── 📄 bg_gradient.xml     # 🎨 Fundo em gradiente
                ├── 📄 ic_camera.xml       # 📸 Ícone vetorial da câmera
                └── 📄 ic_videocam.xml     # 🎥 Ícone vetorial do vídeo
```

---

## 🚀 Como Executar

### 📋 Pré-requisitos

| Requisito | Detalhe |
|:----------|:--------|
| **Android Studio** | Versão **Hedgehog** ou superior, instalada e configurada. |
| **JDK** | Versão **11 ou superior** (geralmente incluído no Android Studio). |
| **Dispositivo ou Emulador** | Android físico (USB + depuração ativada) ou AVD com câmera configurada. |

---

### 🔧 Passo a Passo

**1. Clone o repositório:**

```bash
git clone https://github.com/VictorHJesusSantiago/appcamera.git
```

**2. Abra no Android Studio:**

```
Android Studio → File → Open → Selecione a pasta 'appcamera'
```

**3. Sincronize o Gradle:**

```
Build → Sync Project with Gradle Files
```

> O Android Studio detectará o projeto e fará o download das dependências automaticamente.

**4. Execute a aplicação:**

```
Run → Run 'app'  (ou clique no botão ▶️ na barra de ferramentas)
```

**5. Conceda as permissões:**

> Na primeira execução, o sistema Android solicitará as permissões de **câmera** e **áudio**. Conceda-as para habilitar todas as funcionalidades.

---

### 📱 Testando no Emulador

| Funcionalidade | Como Testar no AVD |
|:---------------|:-------------------|
| 📸 **Tirar Foto** | O emulador possui câmera virtual configurável em `Extended Controls → Camera`. |
| 📹 **Gravar Vídeo** | Disponível na câmera virtual do AVD; use `Extended Controls` para simular. |
| 📺 **Reprodução** | O vídeo será reproduzido automaticamente no `VideoView` após a gravação. |

---

## 🤝 Como Contribuir

> Contribuições são muito bem-vindas! Siga as etapas abaixo para colaborar de forma organizada.

| Passo | Ação | Comando |
|:-----:|:-----|:--------|
| 1️⃣ | **Fork** | Crie um fork do repositório para a sua conta. | — |
| 2️⃣ | **Branch** | Crie sua feature branch a partir da `main`. | `git checkout -b feature/NovaFeature` |
| 3️⃣ | **Commit** | Salve as alterações com mensagem clara e semântica. | `git commit -m 'feat: Adiciona NovaFeature'` |
| 4️⃣ | **Push** | Envie a branch para o repositório remoto. | `git push origin feature/NovaFeature` |
| 5️⃣ | **Pull Request** | Abra um PR detalhando as mudanças realizadas. | — |

<div align="center">

<br>

**Se este projeto foi útil para os seus estudos, deixe uma estrela ⭐️ no repositório!**

</div>

---

## 👨‍💻 Autor

<div align="center">

<br>

**Victor H. J. Santiago**

<br>

[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/VictorHJesusSantiago)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/victor-henrique-de-jesus-santiago/)

</div>

---

## 📄 Licença

<div align="center">

Este projeto está distribuído sob a **Licença MIT**.
Consulte o arquivo [`LICENSE`](./LICENSE) no repositório para mais informações.

![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)

</div>

---

<div align="center">

*Feito com 📸 e Java por **Victor H. J. Santiago***

</div>
