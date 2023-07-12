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

## Código completo
´´´
const int botao = 40; 
const int LedVerde = 24;
const int LedLaranja = 25;
int pinosPontos[] = {31,32,33,34,35,36};
int pinosLinhas[]  = {5,3,2,11,12,13};
int pinosColunas[] = {6,7,8,9,10};
int contador;

void setup(){
  for (int nC = 0; nC <= 4  ; nC++){ //define todos os pinos correspondentes às colunas do teclado matricial em saídas ligadas
     pinMode(pinosColunas[nC], OUTPUT);
     digitalWrite(pinosLinhas[nC], HIGH);
  }
  for (int nL = 0; nL <= 5; nL++){
     pinMode(pinosLinhas[nL], INPUT_PULLUP); //define todos os pinos correspondentes às linhas do teclado matricial em entrada
  }  
  pinMode(botao, INPUT_PULLUP);
  pinMode(LedVerde, OUTPUT);
  pinMode(LedLaranja, OUTPUT);
}
void loop(){
  for (int nP = 0; nP <= 5; nP++){ //define todos os pontos ligados às válvulas como saídas ligadas
     pinMode(pinosPontos[nP], OUTPUT);
     digitalWrite(pinosPontos[nP], HIGH); 
  }
  if (contador){
    TecladoAlfabeto();
  }
  else{
    TecladoCela();
  }
  if (!digitalRead(botao)){  //toda vez que o botão é pressionado, altera-se a função dada para o teclado 
    contador = !contador;
    if (contador){ //LED verde ligado, é sinal que a função TecladoAlfabeto está ativa 
      digitalWrite(LedVerde, HIGH);
      digitalWrite(LedLaranja, LOW);
    }
    else{ // co contrário, LED laranja ligado, é sinal que a função TecladoCela está ativa
      digitalWrite(LedLaranja, HIGH);
      digitalWrite(LedVerde, LOW);
    }
    while(!digitalRead(botao)){ //impede que a função se altere se o botão continuar pressionado     
    }
  } 
 delay(100); 
}

void TecladoAlfabeto(){
    for (int nP = 0; nP <= 5; nP++){
     pinMode(pinosPontos[nP], OUTPUT);
     digitalWrite(pinosPontos[nP], HIGH);
  }
     
    //faz varredura em todas as colunas
    for (int nC = 0; nC <= 4; nC++){
      digitalWrite(pinosColunas[nC], LOW);
      
      //faz varredura em todas as colunas verificando se tem algum botao apertado
      for (int nL = 0; nL <= 5; nL++){
        if (digitalRead(pinosLinhas[nL]) == LOW){
            if (pinosLinhas[nL] == 5 && pinosColunas[nC] == 6){ //letra A
            digitalWrite(31,LOW); //aciona o ponto 1
            delay(2000);
            }
            if (pinosLinhas[nL] == 5 && pinosColunas[nC] == 7){ //letra B
            digitalWrite(31,LOW); //aciona o ponto 1
            digitalWrite(32,LOW); //aciona o ponto 2
            delay(2000);
            }                  
            if (pinosLinhas[nL] == 5 && pinosColunas[nC] == 8){  //letra C 
            digitalWrite(31,LOW); //aciona o ponto 1
            digitalWrite(34,LOW); //aciona o ponto 4
            delay(2000);
            }          
            if (pinosLinhas[nL] == 5 && pinosColunas[nC] == 9){ //letra D
            digitalWrite(31,LOW);
            digitalWrite(34,LOW);
            digitalWrite(35,LOW);
            delay(2000);
            }
            if (pinosLinhas[nL] == 5 && pinosColunas[nC] == 10){ //letra E
            digitalWrite(31,LOW);
            digitalWrite(35,LOW);
            delay(2000);
            }
            if (pinosLinhas[nL] == 3 && pinosColunas[nC] == 6){ //letra F
            digitalWrite(31,LOW);
            digitalWrite(32,LOW);
            digitalWrite(34,LOW);  
            delay(2000);
            }                  
            if (pinosLinhas[nL] == 3 && pinosColunas[nC] == 7){ //letra G
            digitalWrite(31,LOW);
            digitalWrite(32,LOW);
            digitalWrite(34,LOW);
            digitalWrite(35,LOW);
            delay(2000);
            }          
            if (pinosLinhas[nL] == 3 && pinosColunas[nC] == 8){ //letra H 
            digitalWrite(31,LOW);
            digitalWrite(32,LOW);
            digitalWrite(35,LOW);
            delay(2000);
            }
            if (pinosLinhas[nL] == 3 && pinosColunas[nC] == 9){ //letra I
            digitalWrite(32,LOW);
            digitalWrite(34,LOW);
            delay(2000);
            }
            if (pinosLinhas[nL] == 3 && pinosColunas[nC] == 10){ //letra J
            digitalWrite(32,LOW);
            digitalWrite(34,LOW);
            digitalWrite(35,LOW);
            delay(2000);
            }
            if (pinosLinhas[nL] == 2 && pinosColunas[nC] == 6){ //letra K
            digitalWrite(31,LOW);
            digitalWrite(33,LOW);
            delay(2000);
            }
            if (pinosLinhas[nL] == 2 && pinosColunas[nC] == 7){ //letra L
            digitalWrite(31,LOW);
            digitalWrite(32,LOW);
            digitalWrite(33,LOW);
            delay(2000);
            }
            if (pinosLinhas[nL] == 2 && pinosColunas[nC] == 8){ //letra  M
            digitalWrite(31,LOW);
            digitalWrite(33,LOW);
            digitalWrite(34,LOW);
            delay(2000);
            }
            if (pinosLinhas[nL] == 2 && pinosColunas[nC] == 9){ //letra N
            digitalWrite(31,LOW);
            digitalWrite(33,LOW);
            digitalWrite(34,LOW);
            digitalWrite(35,LOW);
            delay(2000);
            }
            if (pinosLinhas[nL] == 2 && pinosColunas[nC] == 10){ //letra O 
            digitalWrite(31,LOW);
            digitalWrite(33,LOW);
            digitalWrite(35,LOW);
            delay(2000);
            }
            if (pinosLinhas[nL] == 11 && pinosColunas[nC] == 6){ //letra P
            digitalWrite(31,LOW);
            digitalWrite(32,LOW);
            digitalWrite(33,LOW);
            digitalWrite(34,LOW);
            delay(2000);
            }
            if (pinosLinhas[nL] == 11 && pinosColunas[nC] == 7){ //letra Q
            digitalWrite(31,LOW);
            digitalWrite(32,LOW);
            digitalWrite(33,LOW);
            digitalWrite(34,LOW);
            digitalWrite(35,LOW);
            delay(2000);
            }
            if (pinosLinhas[nL] == 11 && pinosColunas[nC] == 8){  //letra R
            digitalWrite(31,LOW);
            digitalWrite(32,LOW);
            digitalWrite(33,LOW);
            digitalWrite(35,LOW);
            delay(2000);
            }
            if (pinosLinhas[nL] == 11 && pinosColunas[nC] == 9){ //letra S
            digitalWrite(32,LOW);
            digitalWrite(33,LOW);
            digitalWrite(34,LOW);
            delay(2000);
            }
            if (pinosLinhas[nL] == 11 && pinosColunas[nC] == 10){ //letra T 
            digitalWrite(32,LOW);
            digitalWrite(33,LOW);
            digitalWrite(34,LOW);
            digitalWrite(35,LOW);
            delay(2000);
            }
            if (pinosLinhas[nL] == 12 && pinosColunas[nC] == 6){ //letra U
            digitalWrite(31,LOW);
            digitalWrite(33,LOW);
            digitalWrite(36,LOW);
            delay(2000);
            }
            if (pinosLinhas[nL] == 12 && pinosColunas[nC] == 7){ //letra V
            digitalWrite(31,LOW);
            digitalWrite(32,LOW);
            digitalWrite(33,LOW);
            digitalWrite(36,LOW);
            delay(2000);
            }
            if (pinosLinhas[nL] == 12 && pinosColunas[nC] == 8){ //letra W
            digitalWrite(32,LOW);
            digitalWrite(34,LOW);
            digitalWrite(35,LOW);
            digitalWrite(36,LOW);
            delay(2000);
            }
            if (pinosLinhas[nL] == 12 && pinosColunas[nC] == 9){ //letra X
            digitalWrite(31,LOW);
            digitalWrite(33,LOW);
            digitalWrite(34,LOW);
            digitalWrite(36,LOW);
            delay(2000);
            }
            if (pinosLinhas[nL] == 12 && pinosColunas[nC] == 10){ //letra Y
            digitalWrite(31,LOW);
            digitalWrite(33,LOW);
            digitalWrite(34,LOW);
            digitalWrite(35,LOW);
            digitalWrite(36,LOW);
            delay(2000);
            }          
            if (pinosLinhas[nL] == 13 && pinosColunas[nC] == 8){ //letra Z
            digitalWrite(31,LOW);
            digitalWrite(33,LOW);
            digitalWrite(35,LOW);
            digitalWrite(36,LOW);
            delay(2000);
            }
        }
      }
      digitalWrite(pinosColunas[nC], HIGH);
    }
}

void TecladoCela(){
  for (int nC = 0; nC <= 4; nC++){
      digitalWrite(pinosColunas[nC], LOW);
      for (int nL = 0; nL <= 5; nL++){
        if (digitalRead(pinosLinhas[nL]) == LOW){
            if (pinosLinhas[nL] == 5 && pinosColunas[nC] == 6){ //ponto 1 (A)
            digitalWrite(31,LOW);
            delay(2000);
            }
            if (pinosLinhas[nL] == 5 && pinosColunas[nC] == 7){ //ponto 4 (B)
            digitalWrite(34,LOW);
            delay(2000);
            }                  
            if (pinosLinhas[nL] == 3 && pinosColunas[nC] == 6){  //ponto 2 (F)
            digitalWrite(32,LOW);
            delay(2000);
            }          
            if (pinosLinhas[nL] == 3 && pinosColunas[nC] == 7){ //ponto 5 (G)
            digitalWrite(35,LOW);
            delay(2000);
            }
            if (pinosLinhas[nL] == 2 && pinosColunas[nC] == 6){ //ponto 3 (K)
            digitalWrite(33,LOW); 
            delay(2000);
            }
            if (pinosLinhas[nL] == 2 && pinosColunas[nC] == 7){ //ponto 6 (L)
            digitalWrite(36, LOW);
            delay(2000);
            }
          }
        }
        digitalWrite(pinosColunas[nC], HIGH);
    }
}
´´´

## Teorias
### Cegueira, importância do braile e a *desbrailização*
#### Cegueira
A cegueira é caracterizada pela perda total ou parcial da visão, podendo ser permanente ou temporária. Contrariando um equívoco comum, a cegueira não se limita apenas à ausência total de visão, na qual a pessoa não percebe nem mesmo projeções de luz. Existem também casos de cegueira parcial, conhecida como cegueira legal, em que a pessoa consegue enxergar vultos e projeções luminosas. Além disso, existem diferentes condições que podem levar à cegueira, como a ambliopia, caracterizada pela diminuição da visão devido a algum déficit neurológico que ocorre na infância, ou o tracoma, uma forma de conjuntivite bacteriana. Outras causas incluem traumas oculares causados por objetos pontiagudos, queimaduras ou exposição a substâncias químicas. Para lidar com cegueiras irreversíveis, a inclusão é uma opção fundamental, buscando formas de garantir a qualidade de vida das pessoas afetadas. Nesse contexto, o sistema de leitura e escrita braille desempenha um papel fundamental.

#### A importância do braile
O braille é um sistema universal de leitura e escrita, composto por pontos táteis, que se mostra eficiente para a educação e informação de pessoas com deficiência visual. Criado por Louis Braille, ele simplifica o sistema a seis pontos de relevo distribuídos em duas colunas, formando um total de 63 símbolos diferentes. O braille é utilizado em textos literários, em vários idiomas, e também é aplicado em simbologias matemáticas, científicas, musicais e na informática.

A falta de tradução em braille de livros no cotidiano se deve à portaria ministerial nº 504, que proibia a venda desses livros no Brasil, dificultando o incentivo para sua impressão. Além disso, a tecnologia específica e custosa das impressoras braille e o fato de que a escrita em braille ocupa espaço físico, tornando os livros maiores, também são desafios. No entanto, ainda existem livros traduzidos em braille, principalmente didáticos. O braille continua a ser uma ferramenta valiosa para pessoas cegas, possibilitando acesso à comunicação escrita e tornando suas vidas mais práticas e autônomas.

A leitura em braille permite um contato direto com a cultura e o conhecimento, além de facilitar a educação desses indivíduos e simplificar tarefas cotidianas, como operar um elevador ou identificar o banheiro correto. O braille se torna, assim, um instrumento importante para pessoas cegas, proporcionando-lhes acesso à comunicação através da linguagem escrita.

#### *Desbreilização*
De acordo com um artigo de Verônica Soares na revista Minas Faz Ciência, o fenômeno da "desbrailização" está ocorrendo atualmente, resultando na subutilização do Sistema Braille devido aos recursos tecnológicos em áudio. Isso é causado por diversos fatores, como a falta de preparo dos professores, o tempo e os custos envolvidos na produção do Braille, levando à substituição desse sistema por recursos de áudio e até mesmo leitores humanos. Isso tem impactos negativos no processo educacional dos alunos com deficiência visual, pois eles perdem o contato com a palavra escrita, prejudicando, por exemplo, a alfabetização em matemática. A falta de motivação das crianças para aprender Braille está relacionada à facilidade de acesso à informação proporcionada pela tecnologia, resultando em altas taxas de crianças com deficiência visual crescendo sem alfabetização. Estudos mostram que apenas através do Braille o cérebro dos deficientes visuais absorve efetivamente as letras, pontuação e estrutura dos textos.

## Vídeo explicativo
(vídeo)

## Finalização
O projeto foi feito em 2023 no primeiro semestre do curso de BCC, da disciplina de Eletrônica,
na USP de São Carlos, lecionada pelo professor Eduardo do Valle Simoes. 
