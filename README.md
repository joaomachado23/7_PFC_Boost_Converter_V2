# 7_PFC_Boost_Converter_V2

O objetivo deste trabalho foi o design, simulação, conceção e teste de um protótipo funcional de conversor de potência, a apresentar no final do semestre. Todos os grupos tiveram de desenvolver um Conversor CA-CC do tipo Boost PFC, respeitando requisitos de tensão e corrente definidos.

O conversor era constituído por um estágio CA-CC, com transformador abaixador e ponte retificadora de díodos (retificação síncrona), seguido de um estágio CC-CC na topologia Boost com carga resistiva. O estágio Boost operava com um método de controlo do tipo PFC (Power Factor Correction), cujo objetivo é corrigir o fator de potência e reduzir a potência reativa no sistema.

O nosso grupo optou por implementar um protótipo praticamente integrado em PCB, que inclui:

1. Andar de potência (com PGND) — engloba todos os componentes dos estágios CA-CC e CC-CC, incluindo sensores de tensão e de corrente (ambos de efeito Hall), excetuando o transformador, que ficou fora da PCB;

2. Andar de controlo (com SGND) — inclui:

  - Circuitos de alimentação auxiliares: num conector liga-se uma fonte de bancada que fornece ±15 V; essa tensão é depois convertida para 5 V e 3,3 V por reguladores (um conversor buck síncrono e um LDO).
  - Circuito de condicionamento de sinal: um IC com dois amplificadores operacionais em configuração diferencial (sensor de corrente) e em seguidor de tensão (sensor de tensão), filtros analógicos passa-baixo de primeira ordem e proteção para o ADC.
  - Microcontrolador e interface de comunicação série (UART ↔ USB): um STM32G474RET6 incorporado na placa, com os circuitos de alimentação, reset e programação dimensionados conforme a aplicação e o fabricante.

Todo o design foi concebido e verificado em ambiente de simulação (PSIM), tanto ao nível do hardware de potência como da teoria de controlo aplicada. Importa destacar que, nesta iteração, o controlo era linear: o sinal da gate do IGBT apresentava frequência fixa e era gerado por comparação entre uma portadora triangular (frequência e amplitude fixas) e uma moduladora, que corresponde à saída de um controlador PI. Essa moduladora era limitada posteriormente entre 0 e 70 (i.e., duty-cycle fisicamente limitado entre 0% e 70%).

O conversor era controlado por corrente, com referência de corrente do lado da rede (4 Arms). A referência era comparada com o valor instantâneo da corrente na bobina; a diferença constituía a entrada do controlador PI.

Os resultados obtidos foram bastante satisfatórios e promissores, sobretudo tendo em conta que a tecnologia ficou praticamente toda embebida na PCB, incluindo o microcontrolador. Para tornar o conversor independente de fontes de bancada externas, o grupo considerou ser adequado, numa versão futura, ligar um módulo conversor CC-CC isolado à saída da ponte retificadora, tomando os cuidados necessários para não comprometer o objetivo do controlo PFC.

Conteúdos disponíveis neste repositório:

- PDF com toda a documentação do projeto (apresentação): estado da arte, design, simulação, conceção, testes e resultados.

- Ficheiro rar com fotos e vídeos do protótipo.

- Pasta com prints de resultados dos testes ao conversor.

- Ficheiro PSIM (.psimsch) com a simulação do conversor.
  
- Pasta com o projeto da PCB feito em Altium.

Este trabalho foi fundamental para explorar o desafio de integrar toda a tecnologia numa PCB e para consolidar conhecimentos em eletrónica de potência, com foco no hardware de potência, condicionamento de sinal e firmware de controlo. Foi um projeto exigente, dadas todas as condicionantes a ter em atenção e não esquecendo a função principal do conversor, mas foi concluído com sucesso.

Um grande obrigado aos colegas que me acompanharam nesta jornada: Diego Brandão, Francisco Costa, João Santos e Rui Pedroso.
