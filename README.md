# Projeto: Sistema de Sensoriamento para Agricultura

Este repositório contém o modelo de banco de dados e o código desenvolvido para o sistema de sensoriamento de uma plantação. O sistema coleta dados de sensores em tempo real e faz ajustes automáticos na irrigação e aplicação de nutrientes, utilizando uma base de dados Oracle.

## Objetivo

O objetivo do sistema é otimizar o uso de água e nutrientes, ajustando automaticamente a quantidade aplicada com base nos dados coletados por três tipos de sensores (umidade, pH, nutrientes) instalados em diferentes culturas.

## Estrutura do Banco de Dados (MER)

### Entidades e Atributos:

**ENTIDADE SENSOR**
  - **SEN_ID (PK):** Identificador único do sensor.
  - **SEN_TIPO:** Tipo de sensor (ex: umidade, pH, NPK).
  - **SEN_DESCRICAO:** Breve descritivo do tipo de  sensor.

**ENTIDADE CULTURA**
  - **CUL_ID (PK):** Identificador único da cultura.
  - **CUL_NOME:** Nome da cultura (ex: milho, soja).
  - **CUL_UMIDADE_MIN:** Umidade mínima ideal para a cultura.
  - **CUL_UMIDADE_MAX:** Umidade máxima ideal para a cultura.
  - **CUL_PH_MIN:** pH mínimo ideal para a cultura.
  - **CUL_PH_MAX:** pH máximo ideal para a cultura.
  - **CUL_N_MIN:** Nível mínimo de Nitrogenio necessários.
  - **CUL_N_MAX:** Nível máximo de Nitrogenio N necessários.
  - **CUL_P_MIN:** Nível mínimo de Fosforo necessários.
  - **CUL_P_MAX:** Nível máximo de Fosforo necessários.
  - **CUL_K_MIN:** Nível mínimo de Potassio necessários.
  - **CUL_K_MAX:** Nível máximo de Potassio necessários.

**ENTIDADE LEITURA_SENSOR**
  - **LEI_ID (PK):** Identificador único da leitura.
  - **LEI_SENSOR_ID (FK):** Referência ao sensor que fez a leitura.
  - **LEI_CULTURA_ID (FK):** Referência à cultura relacionada à leitura.
  - **LEI_DATA_HORA:** Data e hora da leitura do sensor.
  - **LEI_VALOR:** Valor da leitura (string pois necessita representar valores de NPK).

**ENTIDADE AJUSTE_APLICACAO**
  - **AJU_ID (PK):** Identificador único do ajuste.
  - **AJU_CULTURA_ID (FK):** Referência à cultura que recebeu o ajuste.
  - **AJU_DATA_HORA:** Data e hora do ajuste realizado.
  - **AJU_QUANTIDADE_AGUA:** Quantidade de água aplicada no ajuste.
  - **AJU_QUANTIDADE_NUTRIENTES:** Quantidade de nutrientes aplicados no ajuste (string para representar NPK).

### Relacionamentos

**LEITURA_SENSOR**
  - **SENSOR (1) --- (N) LEITURA_SENSOR:** Um sensor pode ter várias leituras, mas cada leitura é feita por um único sensor.
  - **CULTURA (1) --- (N) LEITURA_SENSOR:** Uma cultura pode ter várias leituras, mas cada leitura está relacionada a uma única cultura.

**AJUSTE_APLICACAO**
  - **CULTURA (1) --- (N) AJUSTE_APLICACAO:** Uma cultura pode ter múltiplos ajustes de aplicação, mas cada ajuste é referente a uma única cultura.

## Diagrama MER

![image](https://github.com/user-attachments/assets/af4d77b4-77a3-4640-bf54-ff7d61232ba4)


## Tecnologias Utilizadas

- **PyCharm** e **SQL Oracle Cloud** para o desenvolvimento do código.
- **Autonomous Transactional Oracle Database** como banco de dados transacional.
- **SQLDesigner** e **Data Modeler** para criar o diagrama de Entidade-Relacionamento (MER).
- **Markdown** para a documentação no GitHub.
- **GitHub** para versionamento de código.

## Configuração do Ambiente de Desenvolvimento

### Requisitos:

1. **Autonomous Transactional Oracle Database** como banco de dados transacional.

### Configuração do Banco de Dados Oracle:

1. Configurar conta Free Tier em https://www.oracle.com/cloud/free/
2. Provisionar **Autonomous Transactional Oracle Database**
3. Abrir SQL Console
4. Executar o script SQL_SCRIP_CAP1_FIAP.sql

Caso queira ajustar/testar o script SQL_SCRIP_CAP1_FIAP.sql, foi gerado o script DROP_ALL.sql que derruba todas as tabelas, dados e views.
