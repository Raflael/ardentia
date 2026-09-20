# Ardentia

> *Ardentia*: o nome que os pescadores dão ao brilho que a água solta à noite
> quando o barco corta o mar.

Um mar noturno que roda no navegador. Está tudo escuro até você encostar na
água: aí o plâncton acende em azul e a luz gira junto com a correnteza.

Há peixes nadando na tela. **Nenhum deles é desenhado.** Você só os enxerga
porque o plâncton acende na água que eles empurram — e quando o cursor chega
perto, eles disparam e deixam um rastro aceso atrás.

Sem bibliotecas, sem build: um arquivo HTML, JavaScript e WebGL2.

## O que é biologia de verdade aqui

O brilho não é enfeite: é um modelo do bicho.

- **Quem acende são dinoflagelados** — algas unicelulares. O gatilho não é
  toque nem luz: é a **taxa de deformação** da água (o cisalhamento) esticando
  a membrana da célula. Por isso a luz nasce onde a água *se deforma*, não onde
  ela simplesmente se move rápido: água correndo em bloco não acende nada.
- **A luz é um recurso que acaba.** Cada célula gasta a luciferina ao piscar e
  leva alguns segundos para refazer o estoque. Agite sempre o mesmo ponto e ele
  vai apagando; volte um minuto depois e ele acendeu de novo.
- **O clarão é rápido e o apagar é lento**, como o pulso real da célula.
- **O escuro é o estado normal.** O mar calmo só solta faíscas esparsas, de
  células que disparam sozinhas.
- A cor fica perto de **475 nm**, o azul-ciano que essa luciferase emite — o
  comprimento de onda que atravessa melhor a água do mar.

## Como funciona, por baixo

- **A água é simulada**, não é ruído animado: um solver de fluido incompressível
  (*Stable Fluids*, Stam 1999) numa grade grossa, com advecção semi-lagrangiana,
  projeção por Jacobi e confinamento de vorticidade — é o que mantém os
  redemoinhos vivos em vez de virar borrão.
- **Dezenas de milhares de organismos** flutuam nessa água, cada um com brilho e
  reserva próprios, atualizados na CPU e desenhados como pontos na GPU.
- **A luz é acumulada em HDR** (textura de ponto flutuante) e passa por um bloom
  de dois níveis antes de virar cor de tela. É daí que vem a sensação de luz
  de verdade: onde muitos acendem juntos, a cor caminha de azul a ciano a
  branco, como na foto de uma onda bioluminescente, em vez de estourar num azul
  chapado.
- **Os peixes são só física.** Um corpo articulado que segue a cabeça como uma
  corrente — a ondulação do nado sai de graça daí — empurrando a água e
  esbarrando nas células. A forma que você vê na tela é a resposta do plâncton.

## Como abrir

Abra o `index.html` no navegador. Não precisa de servidor, instalação nem
conexão. Tela cheia (F11) é melhor.

Precisa de WebGL2, que qualquer navegador atual tem.

## Como testar sem olhar

`requestAnimationFrame` congela no Chrome headless, então a página aceita rodar
a simulação em passos fixos e desenhar só o quadro final:

```
index.html?teste=1&t=4          # simula 4 s com um dedo traçando a água
index.html?teste=1&t=9&dedo=0   # sem dedo: só os peixes
```

No fim ela despeja em `#estat` o número de organismos, o tamanho da grade, o
custo em milissegundos por passo, quantos estão acesos, o cisalhamento máximo e
a reserva média — que é como se ajusta o balanceamento sem depender do olho.

## Estado

Rascunho que nasceu para responder a uma pergunta: *isso impressiona ou não?*
Impressionou, então virou projeto.

A fazer: onda quebrando na praia com a espuma acendendo; alternar noite e dia,
com o dia virando uma lâmina de microscópio dos mesmos organismos; e acabamento
para o dedo no celular.

## Licença

MIT.
