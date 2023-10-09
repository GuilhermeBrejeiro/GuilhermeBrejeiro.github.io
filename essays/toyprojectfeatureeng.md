---
layout: essay
type: essay
title: MLOps Toy Project - Feature Engineering
# All dates must be YYYY-MM-DD format!
date: 2023-12-03
labels:
  - Modularizacao
  - Producao
  - Aprender ensinando
---

## Processo de Engenharia de Recursos
A engenharia de recursos, também conhecida como feature engineering, desempenha um papel crucial na construção de modelos de aprendizado de máquinas. Nesta seção, vou explorar algumas técnicas amplamente utilizadas para transformar os recursos de entrada brutos e aprimorar o desempenho do modelo de previsão de aprovações de cartões de crédito.

## Importação de Configurações
Para realizar a engenharia de recursos, começamos importando as configurações pré-definidas de nosso projeto:

```python
from configs.project_config import FeatureEngineeringConfig
```
A classe 'FeatureEngineeringConfig' do arquivo de configurações 'project_config.py'contém as configurações necessárias para a engenharia de recursos. Essas configurações incluem informações sobre caminhos de arquivos, nomes de colunas e outros detalhes relevantes.

```python
class FeatureEngineeringConfig:
    def __init__(self):
        self.feature_engineering_config = {
            "logging_feature_engineering_path": "credit_approval/logs/feature_engineering.log",
            "target_column": "StatusAprovacao",
            "train_preprocessed_path": f"credit_approval/data/02_train/preprocessed/train_preprocessed_data_{config_version}.csv",
            "eval_preprocessed_path": f"credit_approval/data/03_eval/preprocessed/eval_preprocessed_data_{config_version}.csv",
            "test_preprocessed_path": f"credit_approval/data/04_test/preprocessed/test_preprocessed_data_{config_version}.csv",
            "train_engineered_path": f"credit_approval/data/02_train/engineered/train_engineered_data_{config_version}.csv",
            "eval_engineered_path": f"credit_approval/data/03_eval/engineered/eval_engineered_data_{config_version}.csv",
            "test_engineered_path": f"credit_approval/data/04_test/engineered/test_engineered_data_{config_version}.csv",
            "encoder_path": f"credit_approval/models/encoder/encoder_{config_version}.pkl",
        }

    def get_feature_engineering_config(self):
        return self.feature_engineering_config

```
## Utilização das Configurações
Uma vez importadas as configurações, é hora de aplicá-las em nosso processo de engenharia de recursos. Aqui está um exemplo simples de como podemos acessar as configurações e usá-las

```python
# Apos importar o FeatureEngineeringcConfig, instanciamos sua classe
config = FeatureEngineeringConfig()

# Obtemos as configurações da instancia
feature_engineering_config = config.get_feature_engineering_config()

# E assim podemos acessar qualquer uma das configurações especificas dessa classe
target_column = feature_engineering_config["target_column"]
```

O arquivo 'feature_engineering.py' contém a classe 'FeatureEngineering' que desempenha um papel central na engenharia de recursos. No entanto, as definições de inicialização da classe neste arquivo específico podem envolver uma grande quantidade de variáveis iniciais. Uma boa prática é organizá-las e tornar o código mais legível. Para atingir esse objetivo, utilizamos um decorator chamado 'dataclass'.
O 'dataclass' é uma ferramenta em Python que nos permite definir classes de dados de forma mais concisa e estruturada. Com ele, podemos declarar e organizar as variáveis e atributos da classe de maneira mais eficiente.
Agora, vamos explorar como o 'dataclass' pode ser usado para simplificar e organizar as definições de inicialização da classe 'FeatureEngineering' no projeto.

Aqui estão algumas classes específicas e organizadas que utilizam o decorator 'dataclass':

```python
@dataclasses.dataclass
class DataFeatures:
    train_data_features: pd.DataFrame
    eval_data_features: pd.DataFrame
    test_data_features: pd.DataFrame


@dataclasses.dataclass
class DataTarget:
    train_data_target: pd.DataFrame
    eval_data_target: pd.DataFrame
    test_data_target: pd.DataFrame


@dataclasses.dataclass
class DataEncoded:
    train_encoded: pd.DataFrame
    eval_encoded: pd.DataFrame
    test_encoded: pd.DataFrame

```
Essas classes facilitam a organização e manipulação dos dados do projeto.

Agora, vejamos como aplicamos essas classes nas configurações iniciais da classe central, 'FeatureEngineering':

```python
class FeatureEngineering:
    def __init__(self, config, data=None):

        self.data = data
        self.feature_engineering_config = config
        self.encoders_obj = None
        self.data_features = DataFeatures()
        self.data_target = DataTarget()
        self.data_encoded = DataEncoded()
```

Neste cenário especifíco, o projeto foi estruturado de modo que a engenharia de recursos seja aplicada nas três bases de dados que vêm sendo construídas desde o processo de ingestão. Isso permite a incorporação fácil de novos conjuntos de dados, caso seja necessário, como no caso de futuras entradas

A primeira função dessa classe utiliza a função auxiliar de leitura de dados 'read_data' para ler sequencialmente as três bases:

```python
    def _read_datas(self) -> Tuple[pd.DataFrame, pd.DataFrame, pd.DataFrame]:
        """
        Reads data from train, eval and test paths using read_data function.
        Returns:
            tuple: Tuple containing:
                train_data (pd.DataFrame): Train data.
                eval_data (pd.DataFrame): Eval data.
                test_data (pd.DataFrame): Test data.
        """
        logging.info("Reading data...")
        train_data = read_data(
            self.feature_engineering_config["train_preprocessed_path"],
        )
        eval_data = read_data(
            self.feature_engineering_config["eval_preprocessed_path"],
        )
        test_data = read_data(
            self.feature_engineering_config["test_preprocessed_path"],
        )
        logging.info("Data read successfully.")

        return train_data, eval_data, test_data

```
O próximo passo na classe é o tratamento dos dados que o modelo preverá no futuro. Esses dados estão no formato de "+" e "-", o que não é aconselhável para modelos de machine learning. Portanto, eles serão convertidos nos valores binários 1 e 0.

Esta função não só realiza a conversão para valores binários, mas também divide a base em variáveis preditoras e váriaveis de resposta. Embora idealmente cada função deve ter apenas uma responsabilidade, neste caso, manteremos essas funcionalidades juntas por enquanto.

```python
    def _split_and_encode_target(
        self, train_data: pd.DataFrame, eval_data: pd.DataFrame, test_data: pd.DataFrame
    ) -> None:
        """
        Splits the data into train, eval and test sets and encodes
        the target column.
        Change the target columns values from + and - to 1 and 0. Then,
        split the data into features and target.
        Args:
            train_data (pd.DataFrame): Train data.
            eval_data (pd.DataFrame): Eval data.
            test_data (pd.DataFrame): Test data.
        """
        logging.info("Encoding target column...")
        # For loop to replace + and - with 1 and 0
        for data in [train_data, eval_data, test_data]:
            data[self.feature_engineering_config["target_column"]] = data[
                self.feature_engineering_config["target_column"]
            ].replace({"-": 0, "+": 1})
        # Split data into features and target
        logging.info("Splitting data into features and target...")
        target_column = self.feature_engineering_config["target_column"]
        self.data_features.train_data_features = train_data.drop(
            target_column,
            axis=1,
        )
        self.data_target.train_data_target = train_data[target_column]
        self.data_features.eval_data_features = eval_data.drop(
            target_column,
            axis=1,
        )
        self.data_target.eval_data_target = eval_data[target_column]
        self.data_features.test_data_features = test_data.drop(
            target_column,
            axis=1,
        )
        self.data_target.test_data_target = test_data[target_column]

```

Dentro dos diversos processos de engenharia de recursos que podem ser aplicados, no modelo em questão, serào utilizadas duas técnicas essenciais: o MinMaxScaler para as colunas com valores numéricos e o OneHotEncoder para as colunas com valores categoricos.

**MinMaxScaler:**
O MinMaxScaler é uma técnica de pré-processamento usada para dimensionar valores numéricos para um intervalo específico, geramente entre 0 e 1. Isso é feito transformando os valores originais em novos valores, onde o valor mínimo se torna o 0 e o valor máximo se torna o 1, mantendo a relação relativa entre os valores originais. Essa técnica é especialmente útil quando se trabalha com algoritmos sensíveis ã escala, como redes neurais e modelos baseados em distância, como K-Means.

**OneHotEncoder:**
O OneHotEncoder é uma técnica usada para lidar com colunas que contém valores categóricos, como cores, tipos de veículos ou categorias de produtos. Ele transforma essas colunas em vetores binários (0s e 1s), onde cada categoria se torna uma nova coluna com um valor binário indicando a presença ou ausência da categoria. Isso é útil porque muitos algoritmos de machine learning não funcionam bem com valores categóricos diretamente; eles exigem representações numéricas. O OneHotEncoder é uma abordagem comum para resolver esse problema e garantir que as categorias não sejam erroneamente interpretadas como valores numéricos contínuos.

No contesto da engenharia de recursos do modelo de aprovações de cartões de crédito, essas técnicas são essenciais para garantir que os dados de entrada sejam formatados de maneira adequada e escalados corretamente antes de alimentar o modelo de machine learning.

```python
    def get_object_and_numeric_columns(self) -> Tuple[pd.Index, pd.Index]:
        """
        Returns the object and numeric columns. Reads the train preprocess data
        and drops the target column. Then, it gets the columns with dtype "object"
        and "number". Returns a tuple containing the object and numeric columns.
        Returns:
            tuple: Tuple containing:
                object_columns (pd.Index): Object columns.
                numeric_columns (pd.Index): Numeric columns.
        """
        # Read train preprocess data
        data_columns = read_data(
            self.feature_engineering_config["train_preprocessed_path"]
        )
        # Drop target column
        data_columns = data_columns.drop(
            self.feature_engineering_config["target_column"],
            axis=1,
        )
        # Get columns with dtype "object"
        object_columns = data_columns.select_dtypes(
            include=["object"],
        ).columns
        # Get columns with dtype "number"
        numeric_columns = data_columns.select_dtypes(
            include=["number"],
        ).columns

        return object_columns, numeric_columns

```

A função 'get_transformer_data_object' utiliza a função auxiliar 'get_object_and_numeric_columns' para distinguir entre colunas numéricas e categóricas. Em seguida, ela cria pipelines separados para cada tipo de variável e aplica o tratamento apropriado.


```python
    def get_transformer_data_object(self) -> ColumnTransformer:
        """
        Returns a ColumnTransformer object that encodes
        categorical features and scales numeric features. It
        uses OneHotEncoder to encode categorical features and
        MinMaxScaler to scale numeric features.
        Returns:
            ColumnTransformer: ColumnTransformer object.
        """
        object_columns, numeric_columns = self.get_object_and_numeric_columns()
        # Create pipelines for encoding categorical features
        # and scaling numeric features
        object_pipeline = Pipeline(
            steps=[
                (
                    "onehot",
                    OneHotEncoder(
                        handle_unknown="ignore",
                        sparse=False,
                    ),
                )
            ]
        )

        numeric_pipeline = Pipeline(
            steps=[
                (
                    "scaler",
                    MinMaxScaler(),
                )
            ]
        )

        encoders = ColumnTransformer(
            transformers=[
                (
                    "object",
                    object_pipeline,
                    object_columns,
                ),
                (
                    "numeric",
                    numeric_pipeline,
                    numeric_columns,
                ),
            ]
        )

        return encoders

```

A seguir, apresentamos a função 'encode_and_convert_dataset', que aplica a função 'get_transformer_data_object'. Ao fazer isso, usamos 'fit_transform' na base de treinamento e apenas o 'transform' nas bases seguintes. Essa abordagem simula um cenário realista em que os dados de treinamento são os únicos dados disponíveis inicialmente, e os dados subsequentes representam novas entradas que o modelo nunca viu antes.
É fundamental aplicar somente o 'tranform'nas bases seguintes, uma vez que desejamos que esses dados futuros sigam as mesmas transformações e escalas que foram aprendidas a partir da base de treinamento. Dessa forma, garantimos que todas as variáveis e escalas estejam alinhadas com o modelo e que os dados futuros sejam tratados de maneira consistente, conforme os padrões estabelecidos durante o treinamento. Essa estratégia contribui para a generalização adequada do modelo e resultados confiáveis quando novos dados forem introduzidos.

```python
    def _encode_and_convert_datasets(
        self,
    ) -> Tuple[pd.DataFrame, pd.DataFrame, pd.DataFrame]:
        """
        Encode train, eval and test datasets and convert them
        to pandas dataframe.
        Returns:
            train_encoded (pd.DataFrame): Encoded train data.
            eval_encoded (pd.DataFrame): Encoded eval data.
            test_encoded (pd.DataFrame): Encoded test data.
        """
        logging.info("Encoding data...")
        # Get encoders
        self.encoders_obj = self.get_transformer_data_object()
        # Fit and transform data
        train_encoded = self.encoders_obj.fit_transform(
            self.data_features.train_data_features
        )
        eval_encoded = self.encoders_obj.transform(
            self.data_features.eval_data_features
        )
        test_encoded = self.encoders_obj.transform(
            self.data_features.test_data_features
        )
        logging.info("Data encoded successfully.")
        logging.info("Converting numpy array to pandas dataframe...")
        self.data_encoded.train_encoded = self._np_to_df(
            train_encoded, self.encoders_obj
        )
        self.data_encoded.eval_encoded = self._np_to_df(
            eval_encoded,
            self.encoders_obj,
        )
        self.data_encoded.test_encoded = self._np_to_df(
            test_encoded,
            self.encoders_obj,
        )
        logging.info("Data converted successfully.")

```

Com isso, os processos de engenharia de recurso representam a etapa final antes do treinamento do modelo. Agora, nossas variáveis de resposta estão no formato binário, as variáveis categóricas foram codificadas e as variáveis numéricas estão em uma escala uniforme. Esse preparo dos dados é fundamental para garantir que o modelo seja capaz de aprender e generalizar a partir das informações disponíveis, resultando em previsões mais precisas e confiáveis.
