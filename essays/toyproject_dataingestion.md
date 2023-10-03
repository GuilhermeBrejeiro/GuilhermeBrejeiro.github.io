---
layout: essay
type: essay
title: MLOps Toy Project - Data Ingestion
# All dates must be YYYY-MM-DD format!
date: 2023-12-01
labels:
  - Modularizacao
  - Producao
  - Aprender ensinando
---

## Automatizando a Aprovação de Cartões de Crédito: De Projeto de Estudos a um Modelo de MLOps

Há alguns anos, enquanto estudava Data Science, fiz um projeto que envolvia a análise de aprovações de cartões de crédito. Na época, utilizei uma base de dados contendo o histórico de solicitações de clientes e os resultados de suas aprovações ou negações. À medida que o tempo passou, percebi que esse projeto poderia ir além do que inicialmente foi criado.

O projeto original foi desenvolvido em um ambiente de Jupyter Notebook e consistia em uma análise exploratória de dados (EDA), pré-processamento, treinamento e avaliação de um modelo de machine learning. Os dados utilizados foram armazenados em um arquivo CSV em meu próprio computador.

Aqui, neste Toy Project, o foco não é criar um modelo de previsão de cartões de crédito mais avançado ou aprofundar a análise exploratória, até por conta de eu não focar meus estudos nessa parte. Em vez disso, estou pegando o projeto original e trabalhando nele para levá-lo a um novo patamar de maturidade e eficiência.

Meu objetivo principal é automatizar o processo de aprovação de cartões de crédito, aplicando as práticas de engenharia de software e consequentemente de MLOps. Vou começar pela modularização do código, transformando o Jupyter Notebook em um conjunto de módulos Python independentes, cada um com uma função especifica.

Além disso, estou construindo um sistema de testes, incluindo testes unitários e, futuramente, de integração, para garantir que cada componente funcione perfeitamente. Isso é essencial para manter a qualidade do código ao longo do tempo.

Outro passo importante é estabelecer uma esteira de integração contínua (CI) que automatize os testes e implantações sempre que houver atualizações no código. Isso garante que o projeto esteja sempre funcionando de maneira confiável.

À medida que avanço, estou explorando opções de implantação em nuvem, como AWS ou GCP, para tornar o projeto mais escalável e adequado para uso em produção.


## Modularizando a Ingestão de Dados

imagem do jupyter notebook carregando os dados de um arquivo csv com o pandas e em seguida a descrição das colunas

Nesse projeto, a primeira etapa é a ingestão de dados. No Jupyter Notebook, esse conjunto de dados foi carregado de um arquivo local. Embora isso funcione bem para um pequeno projeto ou experimento, é importante considerar a escalabilidade e a manutenção do código, especialmente em projetos mais complexos ou em ambiente de produção. Aqui, apesar de nesse primeiro momento eu continuar lendo os dados localmente, já foi criado uma estrutura para que, futuramente, seja bem simples a transição para a leitura de maneira remota, como de um bucket no S3 da AWS.

## Dividindo o Módulo de Ingestão de Dados
O módulo de ingestão de dados foi chamado de 'data_ingestion.py', abaixo uma breve explicação sobre a classe e as funções pertencentes a ela:

A classe foi chamada de DataIngestion, lembrando ser uma boa prática utilizar o nome da classe dessa maneira, letras maiusculas em cada palavra, inclusive a primeira, e sem separação:

```python
class DataIngestion:
    """
    Reads the data, splits it into train, eval and test sets, and saves the data to files.
    """

    def __init__(self, config: dict):
        """
        Initializes the DataIngestion class.
        Args:
            config (DataIngestionConfig): Configuration object.
        """
        self.data_ingestion_config = config
```

O argumento inicial dessa classe é um dicionario de configurações, todas as configurações, parametros e caminhos foram salvas em um arquivo a parte chamado project_config.py, contendo uma classe para cada etapa do projeto, nesse caso a classe DataIngestionConfig:

```python
from configs.project_config import DataIngestionConfig
```
O conteudo importado do project_config.py, nesse modulo, será:

```python
class DataIngestionConfig:
    def __init__(self):
        self.data_ingestion_config = {
            "logging_data_ingestion_path": "credit_approval/logs/data_ingestion.log",
            "external_data_path": "credit_approval/data/00_external_data/cc_approvals.data",
            "raw_path": f"credit_approval/data/01_raw/raw_data_{config_version}.csv",
            "train_path": f"credit_approval/data/02_train/raw/train_data_{config_version}.csv",
            "eval_path": f"credit_approval/data/03_eval/raw/eval_data_{config_version}.csv",
            "test_path": f"credit_approval/data/04_test/raw/test_data_{config_version}.csv",
            "columns": [
                "Genero",
                "Idade",
                "Divida",
                "Casado",
                "ClienteBanco",
                "NivelDeEducacao",
                "Etnia",
                "AnosEmpregado",
                "RegistroAnterior",
                "Empregado",
                "PontuacaoDeCredito",
                "CartaDeMotorista",
                "Cidadao",
                "CodigoPostal",
                "Renda",
                "StatusAprovacao",
            ],
        }
```

Dentro da classe DataIngestion, temos as funções abaixo:

```python
    def split_data(
        self, data: pd.DataFrame
    ) -> Tuple[pd.DataFrame, pd.DataFrame, pd.DataFrame]:
        """
        Splits the data into train, eval and test sets.
        Args:
            data (pd.DataFrame): Data to be split.
        Returns:
            pd.DataFrame: Train set.
            pd.DataFrame: Eval set.
            pd.DataFrame: Test set.
        """
        train, test = train_test_split(data, test_size=0.15, random_state=42)
        train, eval = train_test_split(train, test_size=0.15, random_state=42)

```
A função 'split_data' é responsável por dividir o conjunto de dados em conjutos de treinamento, validação e teste. Isso é crucial para avaliar o desempenho do modelo.

```python
    def _split_and_save_data(self) -> None:
        """
        Splits the data into train, eval and test sets and saves the data to files.
        """

        train, eval, test = self.split_data(self.data)

        # Save train, eval and test sets to files
        logging.info(f"Saving train data to {self.data_ingestion_config['train_path']}")
        write_data(train, self.data_ingestion_config["train_path"])

        logging.info(f"Saving eval data to {self.data_ingestion_config['eval_path']}")
        write_data(eval, self.data_ingestion_config["eval_path"])

        logging.info(f"Saving test data to {self.data_ingestion_config['test_path']}")
        write_data(test, self.data_ingestion_config["test_path"])
```
A função '_split_and_save_data' utiliza a função anterior, 'split_data', para dividir o conjunto de dados e, em seguida, salva os conjuntos de treinamento, validação e testes em arquivos separados.

```python
    def initialize_data_ingestion(self) -> None:
        """
        Reads the data, splits it into train, eval and test sets,
        and saves the data to files.
        """

        try:
            logging.info("Initializing data ingestion...")
            # Read data
            self.data = read_data(self.data_ingestion_config["external_data_path"])

            # Column names
            column_names = self.data_ingestion_config["columns"]

            # Adding column names to the dataframe
            self.data.columns = column_names

            logging.info(f"Saving raw data to {self.data_ingestion_config['raw_path']}")
            write_data(self.data, self.data_ingestion_config["raw_path"])

            logging.info("Splitting data into train, eval and test sets...")
            self._split_and_save_data()
            logging.info("Data ingestion completed.")

        except Exception as e:
            logging.error("Data ingestion failed.")
            raise ExceptionError(e)

```
E finalmente, a função 'initialize_data_ingestion' é a função principal que coordena o processo de ingestão de dados. Ela lê os dados brutos, adiciona nomes de colunas, salva os dados brutos e, em seguida, chama a função '_split_and_save_data' para dividir e salvar os conjuntos de treinamento, validação e teste.

Esta modularização torna o projeto mais organizado e permite que nos concentremos em outras partes do fluxo de trabalho, como pré-processamento, engenharia de recursos, treinamento de modelos e avaliação, sem nos preocuparmos com detalhes de implementação de ingestão de dados. Além disso, se quisermos alterar a fonte de dados no futuro, podemos fazer isso facilmente dentro desse modulo, mantendo o restante do código intacto.

Com a ingestão de dados modularizada, podemos prosseguir para a próxima etapa do projeto: o pré-processamento de dados. Nessa fase, aconteced a limpeza adicional dos dados, tratamento de valores ausentes e preparação dos dados para o treinamento do modelo.
