# Consegui executar (abrir) o Logisim Evolution com Termux:X11

## Instruções para execução (tudo já instalado)

1. No celular, abrir o Termux:X11 Companion app - isto vai criar um console gráfico que receberá os comandos vindos do servidor X;
2. Abrir o termux, executar `termux-x11 :1 -xstartup "dbus-launch --exit-with-session xfce4-session"` - isto vai iniciar o servidor X com XFCE e enviar as mensagens gráficas para o companion app (console), consequentemente o console do X11 Companion App vai mostrar uma janela XFCE.
4. Na janela xfce, CTRL-ALT-T abre um terminal
5. Executar `cd storage/downloads`
6. Executar `java -jar logisim-evolution-4.1.0-all.jar` - a janela do logisim-evolution deve abrir.

## Instruções para instalação

Uso um S24FE, nele instalei Termux, documentei em https://github.com/FNakano/IP-Apostila/tree/main/InstalarTermux .

Em seguida, segui as instruções do gemini, que reproduzo abaixo:

1. No celular, baixar e instalar a versão mais recente do Termux:X11 Companion app;
   - O App Termux:X11 equivale a uma tela de um computador. Nessa tela o ambiente gráfico (ex. XFCE) será exibido. 
   1. Go to the Termux:X11 GitHub Releases page: github.com/termux/termux-x11/releases.Download the .apk that matches your device's architecture (app-arm64-v8a-debug.apk no S24FE). Para instalar tem que desativar alguns bloqueios de segurança no android.
2. No celular, iniciar o Termux, atualizar os pacotes e instalar Termux:X11 e XFCE;
   1. Update package lists - execute `pkg update && pkg upgrade`
   2. Install the X11 repository and the Termux:X11 package - execute
      1. `pkg install x11-repo`
      2. `pkg install termux-x11-nightly`
      3. `pkg install xfce4`
3. Abrir o Companion app - isto vai criar um console gráfico que receberá os comandos vindos do Termux. Voltando ao Termux, executar `termux-x11 :1 -xstartup "dbus-launch --exit-with-session xfce4-session"` - isto vai iniciar o servidor X com XFCE e enviar as mensagens gráficas para o console, consequentemente o console do X11 Companion App vai mostrar uma janela XFCE.
4. Na janela xfce, CTRL-ALT-T abre um terminal por onde executei `pkg install jdk21`, entrei na pasta storage/downloads e executei `java -jar logisim-evolution-4.1.0-all.jar`
   - Notei que há algum problema com a troca de foco dentro e fora do Companion App. Quando uso algum aplicativo do Android, trocando o foco, e volto para o Companion App, os eventos de mouse, como os botões de maximizar, param de funcionar. Por sorte, os atalhos de teclado continuam funcionando então abrir um novo terminal restaura o funcionamento dos eventos de mouse.

# Meu diário sobre como usar Termux:X11

Desejo executar Logisim usando Termux.

Isto me pouparia de carregar notebook quando preciso do Logisim.

Logisim (https://cburch.com/logisim/pt/download.html) é um programa simulador de circuitos lógicos. Esse programa é distribuído em um `jar` e tem interface gráfica. Uso quando ensino Organização e Arquitetura de Computadores.

Termux (https://termux.dev/en/) é um emulador de terminal UNIX para sistema operacional Android. Termux não implementa interface gráfica nem Java. Estes são pacotes instalados separadamente, através do gerenciador de pacotes do Termux (`pkg`).

Combinando Termux com Logisim com algumas outras partes poderia permitir que eu executasse Logisim em um telefone celular com SO Android. A parte que é claro que precisarei é uma interface gráfica. Há alternativas como Termux:X11 (https://github.com/termux/termux-x11) e Termux GUI (https://f-droid.org/pt_BR/packages/com.termux.gui/). A documentação desta última informa que não é compatível com X11.

As instruções e vídeos sobre como instalar e usar Termux:X11 não me ajudam a decidir o que fazer pois uns instruem a instalar proot, debian e xfce (https://www.youtube.com/watch?v=mXkXzFqSeYE), Gemini recomenda instalar ou X11 ou VNC mas as instruçoes me parecem embaralhadas, as instruções em https://github.com/termux/termux-x11 parecem ser fáceis demais para ser verdade... pretendo segui-las, quando tiver tempo.

Existem programas equivalentes ao Logisim, inclusive uma versão web do Logisim (https://logisim.app/). Testei com meu circuito mais complicado, ele executou... talvez eu deva considerar essa alternativa.

Não vi na Internet tutorial mostrando como executar logisim no celular usando Termux.

Há alguma informação que era difícil de encontrar antes da IA (LLM) como Gemini integrada ao buscador Google. Uma delas era saber qual a arquitetura do processador para saber qual apk de Termux:X11 baixar e instalar no telefone. Dentro do Termux, o comando `uname -m` pode retornar aarch64 ou armv7l ou armv8l. aarch64 corresponde a arm64-v8a, armv7l e armv8l correspondem a armeabi-v7a referência em https://github.com/termux/termux-x11/issues/43

X11 é um padrão para comunicação com telas gráficas e dispositivos de entrada. A comunicação é baseada no modelo cliente-servidor onde, para referencial, o servidor tem os dispositivos conectados e envia ao cliente eventos ( ex.: de teclado e mouse). O cliente recebe esses eventos e envia ao servidor X comandos para apresentar algo na tela (https://en.wikipedia.org/wiki/X_Window_System). Cliente e servidor podem ser executados no mesmo computador. 

X11 provê primitivas gráficas mas não provê janelas, botões e outros elementos mais elaborados. Estes são providos por gerenciadores de janela (window managers - https://en.wikipedia.org/wiki/Window_manager). Gerenciadores de janela fazem parte de ambientes de trabalho (desktop environments - https://en.wikipedia.org/wiki/Desktop_environment). É neste ponto que entram nomes conhecidos (para mim) como KDE, GNOME, XFCE (https://en.wikipedia.org/wiki/Xfce), ...

Com a informação até aqui, dá para acreditar que instalar XFCE sobre Termux:X11 é suficiente para executar o Logisim... desde que a implementação de Java para Termux dê suporta a interface gráfica através de X11 o que parece que é verdade. 

![](./Captura%20de%20tela%20de%202026-04-16%2011-34-41.png)


Caso não funcione, a alternativa seria instalar uma distribuição Linux usando Proot ou CHRoot... agora entendi para que Proot serve (simular que o usuário padrão do Termux é root através da implementação dos comandos de root, é parecido com um container ou um venv). Sim, Android tem modo root e (acho que) Termux é capaz de aproveitar essa característica mas habilitar o modo root no Android tem efeitos na garantia e na segurança (Knox) em certas marcas de telefone celular por isso não pretendo tentar um root de verdade).

### Outras anotações

Mudar o tamanho da fonte no termux pode ser feito com *pinch to zoom* ou com CTRL-ALT-+ é diferente do terminal do Linux que é CTRL-SHIFT-+ .

O modo DEX não é iniciado automaticamente quando não é detectada tela, seja com fio, seja sem fio. Quando o hub usb tem conectada a tela através do conector HDMI e o carregador através do conector usb-c e, depois, é ligado ao telefone (S24FE) a tela não é detectada. Desligando o carregador a tela é detectada e, então, o carregador pode ser conectado.


