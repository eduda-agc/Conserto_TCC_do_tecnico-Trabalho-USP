# Conserto_TCC_do_tecnico-Trabalho-USP
#### Disciplina de Eletrônica_2023

## Resumo do Projeto
O projeto consiste consertar um projeto de tcc que se resumia em um tradutor de Braille que permite aos usuários digitar uma letra do alfabeto e imprimir sua respectiva imagem em Braille usando mini válvulas solenoides. Para iniciar a manipulação do dispositivo, é necessário pressionar o botão "função" para que a máquina seja ativada. Uma vez iniciado, o LED azul inicia a função de mapeamento, que ativa cada ponto da célula Braille individualmente, de acordo com a entrada do teclado. Se o botão "função" for pressionado novamente, o LED verde é ativado, liberando a função principal do tradutor, o "Alfabeto Braille". Esse projeto busca fornecer uma solução prática e eficiente para a tradução de letras em Braille, permitindo uma melhor comunicação e acessibilidade para pessoas com deficiência visual.

## Tabela de Preços da produção na época - 2021
| Qtd. | Componentes                | Preço Unidade | Valor Total |
|-----:|:--------------------------:| -------------:| -----------:|
| 1    | Placa de fenolite          | R$ 13,00      | R$ 13,00    |
| 1    | Pacote 100 botões 6x6      | R$ 28,99      | R$ 28,99    | 
| 1    | Jumpers para Arduino (m/m) | R$ 6,00       | R$ 6,00     |
| 1    | Jumpers para Arduino (f/f) | R$ 6,00       | R$ 6,00     |
| 1    | Jumpers para Arduino (m/f) | R$ 6,00       | R$ 6,00     |
| 1    | Fonte bivolt (12V/2A)      | R$ 20,00      | R$ 20,00    |
| 6    | Mini Solenoide (12V/300mA  | R$ 38,43      | R$ 230,58   |
| 6    | Módulo relé 1 canal        | R$ 6,55       | R$ 39,30    |
| 1    | Arduino Mega 2560 R3       | R$ 78,00      | R$ 78,00    |
| 1    | Bateria 9V                 | R$ 22,00      | R$ 22,00    |
| 1    | Caixa de acrílico          | R$ 85,00      | R$ 85,00    |
| -    | Valor total:               | -             | R$ 534,87   |

## Imagem do circuito


## Funcionalidades
+ **Teclado:** O teclado matricial é um dispositivo composto por uma matriz de botões que representa as letras do alfabeto inglês e um botão de função adicional. Ao pressionar um botão, o circuito identifica a posição e envia um sinal para acionar as mini válvulas solenóides correspondentes, que imprimem os pontos do braille. O botão de função permite escolher entre dois modos: um que aciona cada mini válvula solenóide individualmente e outro que imprime a imagem em braille completa de cada letra.
  
+ **Reles de Arduino:** Os relés são dispositivos eletromecânicos que atuam como interruptores controlados por corrente elétrica. No circuito de tradução de letras em braille, eles são essenciais para controlar as mini válvulas solenóides. Cada relé é associado a uma válvula solenóide e, quando energizado, aciona os contatos para permitir a passagem de corrente elétrica e acionar a válvula correspondente. Os relés desempenham um papel crucial ao isolar e proteger o controle de corrente de alta potência, proveniente das mini válvulas solenóides, garantindo um controle individualizado e preciso da impressão dos pontos do braille para a tradução das letras do alfabeto.

+ **Arduino MEGA:** O Arduino Mega 2560 é semelhante ao Arduino Uno, mas oferece maior capacidade de memória, tornando-o adequado para projetos maiores. Além disso, possui um maior número de pinos de entrada e saída, o que foi o fator decisivo para sua utilização. Suas especificações incluem um microcontrolador ATmega2560, operação a 5V, faixa de tensão de entrada de 7V a 12V, 16 portas analógicas e 54 portas digitais (sendo 15 delas utilizáveis como PWM - Modulação por Largura de Pulso).

+ **Minis Solenoides - Pontos da Cela Braille:** As mini válvulas solenóides são dispositivos que convertem energia elétrica em movimento mecânico. No circuito de tradução de letras do alfabeto em braille, elas são acionadas para imprimir os padrões táteis correspondentes aos pontos do braille. Essas válvulas são essenciais para permitir que pessoas com deficiência visual possam ler e compreender informações de forma tátil.

## Link simulador no Tinkercad:

## Projeto do Esquemático
### Teclado Matricial
![Teclado Matricial](https://github.com/eduda-agc/Conserto_TCC_do_tecnico-Trabalho-USP/assets/137100218/3a496ae8-588a-46dd-bd60-ac4e09e8f64d)

### Cadeia dos Módulos dos Relés 
![Cadeia dos Módulos dos Relés](https://github.com/eduda-agc/Conserto_TCC_do_tecnico-Trabalho-USP/assets/137100218/f11e57e2-819f-4c41-ac34-192d7d2e80b1)
#### Rede de conexão de alimentação dos relés
![Rede de conexão de alimentação dos relés](https://github.com/eduda-agc/Conserto_TCC_do_tecnico-Trabalho-USP/assets/137100218/439a8b52-f437-4f9e-919c-84c75462002b)

## Foto do projeto físico
![Imagem do Circuito físico](https://github.com/eduda-agc/Conserto_TCC_do_tecnico-Trabalho-USP/assets/137100218/15c35b6a-c6cc-4ae4-baa7-2a46eef8af20)

## Vídeo explicativo
(vídeo)

## Finalização
O projeto foi feito em 2023 no primeiro semestre do curso de BCC, da disciplina de Eletrônica,
na USP de São Carlos, lecionada pelo professor Eduardo do Valle Simoes. 
