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

A alternativa seria instalar uma distribuição Linux usando Proot ou CHRoot... agora entendi para que Proot serve (simular que o usuário padrão do Termux é root através da implementação dos comandos de root, é parecido com um container). Sim, Android tem modo root e (acho que) Termux é capaz de aproveitar essa característica mas habilitar o modo root no Android tem efeitos na garantia e na segurança (Knox) em certas marcas de telefone celular por isso não pretendo tentar um root de verdade).



