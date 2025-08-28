-- Ativa exibição de mensagens DBMS_OUTPUT
SET SERVEROUTPUT ON;

-- Cria tabela ESTADO para armazenar o estado do motor e dos eixos X/Y
CREATE TABLE ESTADO (
  ATRIBUTO VARCHAR2(10),
  VALOR NUMBER(2)
);

-- Inicializa os valores do veículo
INSERT INTO ESTADO VALUES ('MOTOR', 0);
INSERT INTO ESTADO VALUES ('EIXO X', 0);
INSERT INTO ESTADO VALUES ('EIXO Y', 0);

-- Package que controla operações do veículo
CREATE OR REPLACE PACKAGE VEICULO_PKG AS
  PROCEDURE MOTOR(p_acao VARCHAR2); -- Liga ou desliga o motor
  PROCEDURE MOVIMENTAR(p_eixo CHAR, p_posicoes INT); -- Movimenta eixo X ou Y
  PROCEDURE RESETAR_POSICAO; -- Zera posição dos eixos X e Y
END VEICULO_PKG;
/

-- Implementação das operações do veículo
CREATE OR REPLACE PACKAGE BODY VEICULO_PKG AS

  -- Liga ou desliga o motor e exibe mensagem
  PROCEDURE MOTOR(p_acao VARCHAR2) IS
  BEGIN
    IF UPPER(p_acao) = 'LIGAR' THEN
      UPDATE ESTADO SET VALOR = 1 WHERE ATRIBUTO = 'MOTOR';
      DBMS_OUTPUT.PUT_LINE('MOTOR LIGADO');
    ELSIF UPPER(p_acao) = 'DESLIGAR' THEN
      UPDATE ESTADO SET VALOR = 0 WHERE ATRIBUTO = 'MOTOR';
      DBMS_OUTPUT.PUT_LINE('MOTOR DESLIGADO');
    ELSE
      DBMS_OUTPUT.PUT_LINE('ACAO INVALIDA PARA O MOTOR');
    END IF;
  END MOTOR;

  -- Movimenta o eixo informado, se motor estiver ligado
  PROCEDURE MOVIMENTAR(p_eixo CHAR, p_posicoes INT) IS
    v_motor INT;
    v_atributo VARCHAR2(10);
  BEGIN
    SELECT VALOR INTO v_motor FROM ESTADO WHERE ATRIBUTO = 'MOTOR';
    IF v_motor = 0 THEN
      DBMS_OUTPUT.PUT_LINE('MOTOR DESLIGADO: MOVIMENTO NAO EXECUTADO');
      RETURN;
    END IF;

    IF UPPER(p_eixo) = 'X' THEN
      v_atributo := 'EIXO X';
    ELSIF UPPER(p_eixo) = 'Y' THEN
      v_atributo := 'EIXO Y';
    ELSE
      DBMS_OUTPUT.PUT_LINE('EIXO INVALIDO');
      RETURN;
    END IF;

    UPDATE ESTADO SET VALOR = VALOR + p_posicoes WHERE ATRIBUTO = v_atributo;
    DBMS_OUTPUT.PUT_LINE('MOVIMENTO NO EIXO ' || UPPER(p_eixo) || ' EM ' || p_posicoes || ' POSICOES');
  END MOVIMENTAR;

  -- Zera os valores dos eixos X e Y
  PROCEDURE RESETAR_POSICAO IS
  BEGIN
    UPDATE ESTADO SET VALOR = 0 WHERE ATRIBUTO IN ('EIXO X', 'EIXO Y');
    DBMS_OUTPUT.PUT_LINE('POSICAO ZERADA');
  END RESETAR_POSICAO;

END VEICULO_PKG;
/

-- Sequência de comandos para simular operação do veículo

-- Liga o motor
EXEC VEICULO_PKG.MOTOR('LIGAR');
SELECT * FROM ESTADO;

-- Ponto 1: Move para (1,1)
BEGIN
  VEICULO_PKG.MOVIMENTAR('X', 1);
  VEICULO_PKG.MOVIMENTAR('Y', 1);
END;
/
SELECT * FROM ESTADO;

-- Ponto 2: Move para (2,2)
BEGIN
  VEICULO_PKG.MOVIMENTAR('X', 1);
  VEICULO_PKG.MOVIMENTAR('Y', 1);
END;
/
SELECT * FROM ESTADO;

-- Ponto 3: Move para (4,3)
BEGIN
  VEICULO_PKG.MOVIMENTAR('X', 2);
  VEICULO_PKG.MOVIMENTAR('Y', 1);
END;
/
SELECT * FROM ESTADO;

-- Ponto 4: Move para (6,3)
BEGIN
  VEICULO_PKG.MOVIMENTAR('X', 2);
END;
/
SELECT * FROM ESTADO;

-- Ponto 5: Move para (4,1)
BEGIN
  VEICULO_PKG.MOVIMENTAR('X', -2);
  VEICULO_PKG.MOVIMENTAR('Y', -2);
END;
/
SELECT * FROM ESTADO;

-- Desliga o motor
BEGIN
  VEICULO_PKG.MOTOR('DESLIGAR');
END;
/
SELECT * FROM ESTADO;

-- Reseta posição dos eixos
BEGIN
  VEICULO_PKG.RESETAR_POSICAO;
END;
/
SELECT * FROM ESTADO;
