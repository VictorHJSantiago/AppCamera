<div align="center">
📸 AppCamera - Aplicativo Android 📱

Um aplicativo Android nativo, desenvolvido em Java, que demonstra como acionar a câmara do dispositivo para tirar fotos e gravar vídeos.
</div>

<p align="center"> <img alt="Status do Projeto" src="https://img.shields.io/badge/Status-Completo_(Demo)-brightgreen?style=for-the-badge"> <img alt="Linguagem" src="https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white"> <img alt="Plataforma" src="https://img.shields.io/badge/Android-3DDC84?style=for-the-badge&logo=android&logoColor=white"> <img alt="Build" src="https://img.shields.io/badge/Build-Gradle-02303A?style=for-the-badge&logo=gradle"> </p>

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
📖 Sobre o Projeto

O AppCamera é um projeto de demonstração simples para Android que ilustra uma das funcionalidades mais comuns do sistema: interagir com a câmara.

Em vez de construir uma interface de câmara complexa do zero (usando APIs como CameraX ou Camera2), este aplicativo utiliza Intents do Android (MediaStore) para "despachar" o pedido para a aplicação de câmara nativa do telemóvel.

Após a captura, o aplicativo está configurado para receber o vídeo gravado e exibi-lo diretamente num VideoView na tela principal.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
✨ Funcionalidades Principais

  📸 Tirar Foto:

Um botão que aciona a Intent MediaStore.ACTION_IMAGE_CAPTURE.

Abre a aplicação de câmara padrão do dispositivo para que o utilizador possa tirar uma fotografia.

  📹 Gravar Vídeo:

Um botão que aciona a Intent MediaStore.ACTION_VIDEO_CAPTURE.

Abre a aplicação de câmara no modo de vídeo.

  📺 Exibição de Média:

Após a gravação de um vídeo, o resultado é capturado pelo onActivityResult.

O vídeo é então carregado num VideoView e reproduzido automaticamente.

  🎨 Design Personalizado:

Inclui um fundo em gradiente (bg_gradient.xml) e ícones vetoriais (ic_camera.xml, ic_videocam.xml).

(Nota: Na versão atual do código, a app está preparada para lidar com o retorno do vídeo, mas a captura do retorno da foto (Bitmap) no onActivityResult não está implementada.)

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
🛠️ Tecnologias Utilizadas

Java: Linguagem principal do aplicativo.

Android SDK: Framework nativo para desenvolvimento Android.

XML (Layouts): Usado para definir a interface do utilizador, incluindo os botões e o VideoView.

Android Intents: MediaStore.ACTION_IMAGE_CAPTURE e MediaStore.ACTION_VIDEO_CAPTURE para interagir com a câmara.

  Gestão de Permissões: O AndroidManifest.xml solicita permissões essenciais:

android.permission.CAMERA

android.permission.RECORD_AUDIO

android.hardware.camera (feature)

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
📂 Estrutura do Repositório
appcamera/

│

├── app/

│   ├── build.gradle.kts      # Configurações do módulo 'app' (dependências)

│   ├── src/

│   │   ├── main/

│   │   │   ├── java/com/example/appcamera/

│   │   │   │   └── MainActivity.java   # A lógica principal da aplicação

│   │   │   ├── res/

│   │   │   │   ├── layout/

│   │   │   │   │   └── activity_main.xml # O design da interface (UI)

│   │   │   │   ├── drawable/           # Ícones e o gradiente

│   │   │   │   └── ...

│   │   │   └── AndroidManifest.xml     # Definição de permissões e atividades

│

├── build.gradle.kts          # Configurações do projeto (nível raiz)

└── settings.gradle.kts       # Configurações do Gradle

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
💿 Como Executar o Projeto

Para compilar e executar este projeto, irá precisar do Android Studio.

Clone o repositório: git clone https://github.com/victorhjsantiago/appcamera.git

Abra no Android Studio:

Abra o Android Studio.

Selecione "Open an Existing Project".

Navegue até à pasta appcamera clonada e selecione-a.

Sincronize o Gradle:

Espere o Android Studio indexar os ficheiros e fazer o download das dependências do Gradle (conforme definido em build.gradle.kts).

Execute a Aplicação:

Conecte um dispositivo Android físico (via USB) ou inicie um Emulador (Android Virtual Device).

Clique no botão "Run" (▶️) na barra de ferramentas do Android Studio.

O aplicativo solicitará permissões de câmara e áudio. Após conceder, pode testar os botões.
