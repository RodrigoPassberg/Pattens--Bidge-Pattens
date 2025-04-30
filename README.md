# Exemplo do Padrão de Projeto Bridge em Java

Este repositório contém um exemplo simples em Java que demonstra a aplicação do padrão de projeto estrutural Bridge.

## 1. Descrição do Projeto

Este projeto ilustra o padrão de projeto Bridge usando um exemplo clássico: a separação entre controles remotos (abstrações) e dispositivos eletrônicos (implementações). O objetivo é mostrar como a abstração (a interface do controle remoto) pode variar independentemente da implementação (o tipo de dispositivo controlado - TV, Rádio, etc.).

O padrão Bridge permite desacoplar uma abstração de sua implementação, de modo que ambas possam evoluir separadamente. Isso evita a "explosão de classes" que ocorreria se usássemos herança simples para todas as combinações possíveis (ControleBasicoTV, ControleAvancadoTV, ControleBasicoRadio, etc.).

## 2. Estrutura do Código

O código está organizado da seguinte forma, seguindo a estrutura do padrão Bridge:

*   **Hierarquia de Implementação (Dispositivos):**
    *   `Device.java`: Interface **Implementor**. Define o contrato para todos os dispositivos (ex: `isEnabled()`, `enable()`, `disable()`, `getVolume()`, `setVolume()`, `getChannel()`, `setChannel()`).
    *   `Tv.java`: Classe **ConcreteImplementor**. Implementa a interface `Device` com a lógica específica para uma TV.
    *   `Radio.java`: Classe **ConcreteImplementor**. Implementa a interface `Device` com a lógica específica para um Rádio.

*   **Hierarquia de Abstração (Controles Remotos):**
    *   `Remote.java`: Interface (opcional, mas boa prática) que define as operações básicas do controle remoto (`power()`, `volumeDown()`, `volumeUp()`, etc.).
    *   `BasicRemote.java`: Classe **Abstraction** (ou **RefinedAbstraction**). Implementa a interface `Remote`. Contém uma referência (`protected Device device;`) ao **Implementor** (a "ponte"). Delega as chamadas para o objeto `device`.
    *   `AdvancedRemote.java`: Classe **RefinedAbstraction**. Estende `BasicRemote` adicionando funcionalidades extras (ex: `mute()`), mas ainda utiliza a mesma "ponte" (`device`).

*   **Cliente:**
    *   `Demo.java`: Classe principal (`main`) que demonstra como o cliente utiliza o padrão. Cria instâncias de dispositivos e controles, conecta-os (estabelece a ponte) e interage com a abstração (`Remote`).

## 3. Como Executar

Para compilar e executar este exemplo, você precisará ter o Java Development Kit (JDK) instalado em sua máquina.

1.  **Estrutura de Diretórios (Sugestão):**
    Organize os arquivos `.java` em uma estrutura de pacotes, se desejar (embora para este exemplo simples, possam estar no mesmo diretório). Exemplo:

    ```
    src/
    ├── devices/
    │   ├── Device.java
    │   ├── Radio.java
    │   └── Tv.java
    ├── remotes/
    │   ├── Remote.java
    │   ├── BasicRemote.java
    │   └── AdvancedRemote.java
    └── Demo.java
    ```

2.  **Compilação:**
    Abra um terminal ou prompt de comando, navegue até o diretório `src` (ou o diretório que contém os arquivos `.java` se não usar pacotes) e compile todos os arquivos Java:

    ```bash
    javac */*.java *.java  # Se usar a estrutura de pacotes sugerida
    # ou
    javac *.java          # Se todos os arquivos estiverem no mesmo diretório
    ```

3.  **Execução:**
    Após a compilação bem-sucedida (que criará os arquivos `.class`), execute a classe `Demo` que contém o método `main`:

    ```bash
    java Demo
    ```

4.  **Saída Esperada:**
    Você deverá ver a saída no console mostrando os testes com o controle básico e avançado, operando a TV e o Rádio, e imprimindo seus status.

## 4. Dependências

*   **Java Development Kit (JDK):** Versão 8 ou superior é recomendada para compilar e executar o código Java.

## 5. Propósito do Padrão Bridge

O principal propósito do padrão Bridge é **desacoplar uma abstração de sua implementação para que ambas possam variar independentemente**.

Isso significa que você pode:

*   Modificar ou estender a hierarquia de abstração (ex: adicionar novos tipos de controles remotos) sem afetar as implementações (os dispositivos).
*   Modificar ou estender a hierarquia de implementação (ex: adicionar novos tipos de dispositivos) sem afetar as abstrações (os controles remotos).
*   Evitar uma ligação permanente e rígida entre uma abstração e sua implementação.
*   Ocultar os detalhes da implementação dos clientes que utilizam a abstração.
*   Melhorar a extensibilidade e a manutenibilidade do sistema, especialmente quando múltiplas dimensões de variação existem (como diferentes tipos de controles *e* diferentes tipos de dispositivos).

Em essência, o Bridge promove a composição sobre a herança para conectar as duas hierarquias, resultando em um design mais flexível e modular.
