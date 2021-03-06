# Tarefa de Embarcados

Aqui você encontrará uma pequena explicação sobre o que será esperado para a tarefa de embarcados do Processo Seletivo.

## Objetivo

O principal objetivo da tarefa é familiarizar você com a programação em C, o visual e a estrutura dos arquivos contidos na pasta dos programas da equipe e como fazer o uso de ADC, PWM e GPIO para interagir com elementos físicos.

Você deverá escrever um código que varie a intensidade de um led ao girar um potênciometro. Também deverá implementar um botão que inverta a lógica de variação da intensidade do led.

## Organização do repositório

O repositório dessa tarefinha foi baseado no [STM32ProjectTemplate](https://github.com/ThundeRatz/STM32ProjectTemplate). Acesse o link para saber mais.

## Configurando o Cube

Antes de sair programando, é necessário configurar o arquivo `tarefa_embarcados.ioc`. Para isso, siga as intruções contidas em [Configurando o Cube](cube_configuration.md).

## Estrutura de arquivos

Os arquivos do código se encontram nas pastas `src` (aqui ficam os .c) e `inc` (aqui ficam os .h).

* `mcu.h` e `mcu.c`: Esses arquivos possuem as funções que configuram o microcontrolador, e **NÃO** devem ser editados.

* `utils.h`: Esse arquivo pode ser incluído onde for necessário, ele contém diversas funções matemáticas úteis que podem facilitar muito as contas. Sinta-se à vontade para incrementá-lo!

* `led_control.h` e `led_control.c`: Esses dois arquivos contém a lógica principal do programa. Algumas das funções aqui presentes já foram implementadas, outras ficam a seu cargo.
O `.h` contém a assinatura das funções, e não precisa ser modificado, a não ser que você ache necessário fazer mais funções públicas (ou seja, que podem ser chamadas em outros arquivos).
O `.c` contém a definição do corpo das funções, aqui que você completará as `Funções que devem ser implementadas` (veja mais logo abaixo), e poderá escrever funções privadas (ou seja, que serão utilizadas apenas dentro desse documento).

* `main.c`: Aqui, você deverá fazer a inicialização dos periféricos e o loop principal do programa.

## Funções principais

Seu programa deve utilizar algumas funções já preestabelecidas, sejam elas já completamente implementadas, ou apenas estruturadas para que você modifique da forma que bem entender.

### Funções prontas

1. **mcu_init():**
    Função essencial do programa, está implementada em `mcu.c` Nela serão inicializadados elementos como os pinos do botão e o clock do sistema. Essa função deve ser a primeira coisa a ser chamada no seu código.

2. **adc_init():**
    Função que inicia o ADC do programa, implementada em `led_control.c`. Lembre-se de chamar essa função antes de tentar fazer leituras.

3. **get_adc_result():**
    Função que retorna o valor da última leitura feita pelo ADC, implementada em `led_control.c`.

### Funções que devem ser implementadas

1. **pwm_init():**
    Função que inicia e configura a PWM do programa. Consulte o [STM32Guide](https://github.com/ThundeRatz/STM32Guide) para implementar essa função.

2. **set_led_brightness(uint16_t brightness):**
    Função que configura a PWM enviada para o LED com base no brilho recebido como parâmetro.

3. **Interrupção:**

    A interrupção é uma pequena função que é chamada sempre que algum evento específico ocorre, como o aperto de um botão, exemplo utilizado nesse exercício. Para isso, você deve usar a função:

    ```C
        void HAL_GPIO_EXTI_Callback(uint16_t GPIO_Pin){}
    ```

    Assim, quando o botão é apertado tudo que você escrever dentro da função acontecerá. Essa ferramenta poderosa possibilita a operação de robôs de sumô a distância, mudando estratégias com o simples aperto de um botão (mais especificamente o botão de um app que envia o comando por bluetooth).
