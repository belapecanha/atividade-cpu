# CPU

Esse projeto é uma CPU de 8 bits simplificada,  composta por várias unidades que se comunicam por um mesmo barramento central e consegue executar operações aritméticas seguindo um ciclo de FETCH e EXECUTE.

---

## Unidades

### BUS

O BUS é o caminho central de dados do sistema. Ele conecta todos os componentes, mas só um pode escrever nele por vez, porém vários podem ler ao mesmo tempo. 

### PC — Program Counter

O PC é o registrador que armazena o endereço da próxima instrução a ser executada. Ele manda esse endereço pro barramento, e o MAR usa esse valor pra acessar a memória.

### CU — Control Unit

A CU funciona como um porteiro: ela garante que a informação do BUS seja a mesma por todo o barramento, decidindo quando cada componente pode agir. Ela tem um ring counter dentro, feito com flip-flops D assíncronos que define o funcionamento desse ciclo. Depois de iniciado com o botão, ele conta um bit por vez, e cada estado define quais drivers do sistema estão habilitados.

### MAR

O MAR é o registrador responsável por armazenar o endereço da memória que será acessado em determinado momento. A memória usa o valor presente no MAR pra localizar exatamente qual posição deve ser lida. Existem dois MARs: um pra operações e outro pra operandos.

### IR — Instruction Register

O IR é responsável por armazenar a instrução atual que está sendo executada pela CPU. A partir disso, a CU identifica qual operação deve ser realizada.

### OPERAÇÕES / OPERANDOS (ROM)

São as memórias responsáveis por armazenar o programa da CPU — as instruções e os dados que serão executados. Elas recebem um endereço do MAR e retornam o valor armazenado naquela posição para o bus.

### ALU

A ALU realiza as operações. As operações disponíveis são:

| Operação      | Operandos  | Saída                        |
|---------------|------------|------------------------------|
| Soma          | AC + N     | AC (8 bits)                  |
| Subtração     | AC - N     | AC (8 bits)                  |
| Multiplicação | AC × N     | AC (8 LSB) e MQ (8 MSB)      |
| Divisão       | AC ÷ N     | AC (Resto) e MQ (Quociente)  |
| Shift lógico  | AC         | AC (8 bits)                  |

Onde N é o operando armazenado em memória, AC é o registrador acumulador e MQ é o registrador de multiplicação e quociente.

---

## Ciclo de Fetch

O ciclo de fetch é a etapa em que a CPU busca a próxima instrução que será executada na memória.

O PC contém o endereço da instrução atual → esse endereço é enviado para o MAR → o MAR acessa a memória → a memória retorna o conteúdo desse endereço para o bus → o IR armazena essa instrução.

Enquanto isso, a Unidade de Controle coordena os sinais para garantir que cada componente atue no momento correto.

---

## Ciclo de Execute

O ciclo de execute é a etapa em que a instrução armazenada no IR é interpretada e executada pela CPU.

O valor da instrução no IR → a CU decodifica a instrução e ativa os sinais para realizar a operação → busca um operando na memória → faz a conta pela ALU → retorna no AC/MQ o resultado.

---
## Imagem da minha CPU e ALU
![CPU](/imagem.png)
![ALU](/imagem-alu.png)

## Vídeo

[[LINK DO VÍDEO]](https://youtu.be/h4QjMx7aFXo)
