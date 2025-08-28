# Oracle Vehicle Controller (PL/SQL)

Este projeto demonstra o controle de um veículo imaginário utilizando uma package PL/SQL no Oracle. O sistema permite ligar/desligar o motor, movimentar o veículo nos eixos X e Y, e resetar sua posição. Todas as operações são registradas na tabela `ESTADO`.

## Funcionalidades

- **Ligar/Desligar Motor**: Controle do estado do motor do veículo.
- **Movimentação nos Eixos X e Y**: Permite alterar a posição do veículo.
- **Reset de Posição**: Zera a posição dos eixos X e Y.
- **Mensagens de Status**: Utiliza `DBMS_OUTPUT.PUT_LINE` para informar cada ação no console.

## Estrutura do Projeto

- Criação da tabela `ESTADO`
- Package PL/SQL (`VEICULO_PKG`) com três procedures:
  - `MOTOR(p_acao VARCHAR2)`
  - `MOVIMENTAR(p_eixo CHAR, p_posicoes INT)`
  - `RESETAR_POSICAO`
- Exemplos de comandos para operar o veículo e acompanhar o estado.

## Como executar

1. Execute o script principal em um ambiente Oracle compatível (SQL*Plus, SQL Developer, etc.).
2. Certifique-se de ativar o `SERVEROUTPUT` para visualizar as mensagens.
3. Siga a sequência de comandos para simular a operação do veículo.

## Exemplo de uso

```sql
EXEC VEICULO_PKG.MOTOR('LIGAR');
BEGIN
  VEICULO_PKG.MOVIMENTAR('X', 1);
  VEICULO_PKG.MOVIMENTAR('Y', 1);
END;
/
SELECT * FROM ESTADO;
```

## Autor

Adonay Rocha

## Licença

Este projeto está sob a licença MIT.
