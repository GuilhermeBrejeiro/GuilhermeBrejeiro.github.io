---
layout: essay
type: essay
title: MLOps Toy Project - Data Preprocessing
# All dates must be YYYY-MM-DD format!
date: 2023-12-02
labels:
  - Modularizacao
  - Producao
  - Aprender ensinando
---

## Pré-processamento de Dados

O pré-processamento de dados é uma etapa fundamental na construção de modelos de aprendizado de máquina. Esta fase envolve a preparação dos dados brutos para que possam ser alimentados em algoritmos de Machine Learning. Aqui, vamos modularizar o fluxo de trabalho de pré-processamento de dados feito no Jupyter Notebook com as análises de aprovações de cartões de crédito.
Novamente, iniciamos o processo com as configurações já pré-definidas, que ficam que um arquivo à parte e devem ser importadas:

```python
from configs.project_config import DataPreprocessingConfig
```

Classe DataPreprocessingConfig do arquivo de configurações project_config.py:

```python
class DataPreprocessingConfig:
    def __init__(self):
        self.data_preprocessing_config = {
            "logging_data_preprocessing_path": "credit_approval/logs/data_preprocessing.log",
            "target_column": "StatusAprovacao",
            "unnecessary_columns": ["CartaDeMotorista", "CodigoPostal"],
            "imputation_values_path": f"credit_approval/models/imputation/imputation_values_{config_version}.pkl",
            "train_path": f"credit_approval/data/02_train/raw/train_data_{config_version}.csv",
            "eval_path": f"credit_approval/data/03_eval/raw/eval_data_{config_version}.csv",
            "test_path": f"credit_approval/data/04_test/raw/test_data_{config_version}.csv",
            "train_preprocessed_path": f"credit_approval/data/02_train/preprocessed/train_preprocessed_data_{config_version}.csv",
            "eval_preprocessed_path": f"credit_approval/data/03_eval/preprocessed/eval_preprocessed_data_{config_version}.csv",
            "test_preprocessed_path": f"credit_approval/data/04_test/preprocessed/test_preprocessed_data_{config_version}.csv",
        }

    def get_data_preprocessing_config(self):
        return self.data_preprocessing_config

```

O arquivo preprocessing.py terá a class DataPreprocessing com as devidas funções responsaveis pelo pré-processamento:

```python
class DataPreprocessing:
    """
    Preprocesses the data by replacing question marks with NaNs,
    selecting numeric columns and imputing missing values with
    mean (numeric) or mode (categorical) values.
    """

    def __init__(self, config: DataPreprocessingConfig):
        """
        Initializes the DataPreprocessing class.

        Args:
            config (DataPreprocessingConfig): Configuration object.
        """
        self.data_preprocessing_config: DataPreprocessingConfig = config
        self.numeric_imputation_values: Dict[str, Union[int, float]] = None
        self.categorical_imputation_values: Dict[str, str] = None
        self.numeric_columns: pd.DataFrame = None
        self.categorical_columns: pd.DataFrame = None
        self.features_train: pd.DataFrame = None
        self.target_train: pd.DataFrame = None
        self.features_eval: pd.DataFrame = None
        self.target_eval: pd.DataFrame = None
        self.features_test: pd.DataFrame = None
        self.target_test: pd.DataFrame = None
        self.train: pd.DataFrame = None
        self.eval: pd.DataFrame = None
        self.test: pd.DataFrame = None

```

## Divisão dos Dados e Exclusão de Colunas Desnecessárias

Após análise, no Jupyter Notebook foi concluído que duas das colunas do dataset não seriam necessárias e, portanto, devem ser eliminadas. Feito isso, a base de dados foi dividida entre treino e teste.

```python
# Import train_test_split
from sklearn.model_selection import train_test_split

# Drop the features 11 and 13
cc_apps = cc_apps.drop([11, 13], axis=1)

# Split into train and test sets
cc_apps_train, cc_apps_test = train_test_split(cc_apps, test_size=0.33, random_state=42)
```

Para a modularização e processo desenvolvidos, isso ficou um pouco diferente. Na própria ingestão já é separado os conjuntos de treino, teste e validação, que são salvos em caminhos especificos, portanto diretamente neles serão feito o processo de exclusão das features e separar os dados de features (X) e target (y):

1. Divisão dos Dados em Features e Target

```python
    def _split_into_features_and_target(self) -> None:
        """
        Splits the data into features and target. The target column is specified
        in the configuration file. The data is read from the files specified
        in the configuration file. The data is split into train, eval and test sets.
        """
        logging.info("Splitting data into features and target...")
        train = read_data(self.data_preprocessing_config["train_path"])
        eval = read_data(self.data_preprocessing_config["eval_path"])
        test = read_data(self.data_preprocessing_config["test_path"])

        self.features_train = train.drop(
            self.data_preprocessing_config["target_column"], axis=1
        )
        self.target_train = train[self.data_preprocessing_config["target_column"]]

        self.features_eval = eval.drop(
            self.data_preprocessing_config["target_column"], axis=1
        )
        self.target_eval = eval[self.data_preprocessing_config["target_column"]]

        self.features_test = test.drop(
            self.data_preprocessing_config["target_column"], axis=1
        )
        self.target_test = test[self.data_preprocessing_config["target_column"]]

```
   
2. Processo de exclusão das colunas
```python
    def drop_unnecessary_columns(self) -> None:
        """
        Drops unnecessary columns. The columns to be dropped are specified
        in the configuration file.
        """
        logging.info(
            f"Dropping unnecessary columns: {self.data_preprocessing_config['unnecessary_columns']}"
        )
        self.features_train.drop(
            self.data_preprocessing_config["unnecessary_columns"], axis=1, inplace=True
        )
        self.features_eval.drop(
            self.data_preprocessing_config["unnecessary_columns"], axis=1, inplace=True
        )
        self.features_test.drop(
            self.data_preprocessing_config["unnecessary_columns"], axis=1, inplace=True
        )
```

## Lidando com Valores Ausentes

Como dito anteriormente, aqui tratamos de produtizar o modelo desenvolvido e, portanto, já é entendido que as análises de como os valores ausentes serão tratados já foram feitas. Existem motivos para se usar a média, a mediana ou a moda na substituição de valores, existem motivos para se manter váriaveis mesmo que elas tenham valores ausentes, existem motivos para cada um dos tratamentos e a análise estátistica e exploratória dos dados já ditaram isso. No modelo em questão, foi decidido que os valores preenchidos com "?" serão substituido por NaN, nas colunas de valores númericos os valores ausentes serão substituidos pela média e nas colunas categóricas serão substituidos pela moda.

```python
# Substituindo '?' por NaN
X_train = X_train.replace('?', np.NaN)
X_test = X_test.replace('?', np.NaN)

# Imputação de valores ausentes em colunas numéricas
numeric_columns = X_train.select_dtypes(include=['number'])
X_train[numeric_columns.columns].fillna(X_train[numeric_columns.columns].mean(), inplace=True)
X_test[numeric_columns.columns].fillna(X_train[numeric_columns.columns].mean(), inplace=True)

# Imputação de valores ausentes em colunas categóricas
for col in X_train.columns:
    if X_train[col].dtypes == 'object':
        X_train = X_train.fillna(X_train[col].value_counts().index[0])
        X_test = X_test.fillna(X_train[col].value_counts().index[0])

```

Novamente, no processo de modularização, alguns detalhes serão modificados. Lembrando que, sempre que possível, cada função modularizada deve ter apenas uma função.

1. Substituindo "?" por NaN

```python
    def _replace_question_marks(self) -> None:
        """
        Replaces question marks with NaNs. This is done because the data
        contains question marks instead of NaNs. This is done before
        calculating imputation values because the imputation values
        are calculated based on the data without question marks.
        """
        logging.info("Replacing question marks with NaNs...")
        self.features_train.replace("?", np.nan, inplace=True)
        self.features_eval.replace("?", np.nan, inplace=True)
        self.features_test.replace("?", np.nan, inplace=True)

```
2. Seleciona Colunas Numéricas

```python
    def _select_numeric_columns(self, data: pd.DataFrame) -> pd.DataFrame:
        """
        Selects numeric columns from the data. This is done because
        imputation values are calculated based on the numeric columns.
        Args:
            data (pd.DataFrame): Input data.

        Returns:
            pd.DataFrame: Numeric columns from the input data.
        """
        return data.select_dtypes(include=["number"])

```

3. Seleciona Colunas Categóricas

```python
    def _select_categorical_columns(self, data: pd.DataFrame) -> pd.DataFrame():
        """
        Selects categorical columns from the data. This is done because
        imputation values are calculated based on the categorical columns.
        Args:
            data (pd.DataFrame): Input data.

        Returns:
            pd.DataFrame: Categorical columns from the input data.
        """
        return data.select_dtypes(include=["object"])

```

4. Calculando os valores conforme o tipo de coluna e salvando esses calculos

O calculo dos valores que serão imputados deve ser feito com base apenas no dataset de treino. Não executar essa separação previamente, pode ocasionar o problema conhecido como "data leakage", no qual o modelo acaba por ter acesso a informações da base de teste e validação e com isso performar melhor nelas. Isso é um problema pois, nos dados do mundo real, ele não terá nenhum tipo de informação, tornando as bases de teste e validação diferentes do que se espera do mundo real podendo gerar um modelo com uma péssima performace em produção.

```python
    def calculate_imputation_values(self) -> None:
        """
        Calculates imputation values for numeric and categorical
        columns. Saves the imputation values to a file.
        The imputation values are calculated based on the train set.
        The imputation values are calculated as follows:
        - Numeric columns: mean
        - Categorical columns: mode
        """
        data = self.features_train
        self.numeric_columns = self._select_numeric_columns(data)
        self.numeric_imputation_values = {
            col: data[col].mean() for col in self.numeric_columns.columns
        }

        self.categorical_imputation_values = self._select_categorical_columns(data)
        self.categorical_imputation_values = {
            col: data[col].mode()[0] for col in self.categorical_imputation_values
        }

        # Create directories if they do not exist
        os.makedirs(
            os.path.dirname(self.data_preprocessing_config["imputation_values_path"]),
            exist_ok=True,
        )

        # Save imputation values to a file
        logging.info(
            f"Saving imputation values to {self.data_preprocessing_config['imputation_values_path']}"
        )
        with open(self.data_preprocessing_config["imputation_values_path"], "wb") as f:
            imputation_values = {
                "numeric_imputation_values": self.numeric_imputation_values,
                "categorical_imputation_values": self.categorical_imputation_values,
            }
            pickle.dump(imputation_values, f)

```

5. Imputando os valores de média e moda

Agora com a média e a moda da base de dados de treinamento, esses valores devem ser imputados em todos os conjuntos.
Feito isso, essa nova base de dados sem nenhum valor nulo será salva para ser usada na próxima etapa do processo.

```python
    def impute_values(self) -> None:
        """
        Imputes missing values with mean (numeric) or mode (categorical) values.
        Saves the preprocessed data to a file.
        The preprocessed data is saved to the files specified
        in the configuration file.
        The preprocessed data is saved as follows:
        - Train set: train_preprocessed_path
        - Eval set: eval_preprocessed_path
        - Test set: test_preprocessed_path
        """
        # Impute missing values
        logging.info("Imputing missing values...")
        for col in self.numeric_columns.columns:
            self.features_train[col].fillna(
                self.numeric_imputation_values[col], inplace=True
            )
            self.features_eval[col].fillna(
                self.numeric_imputation_values[col], inplace=True
            )
            self.features_test[col].fillna(
                self.numeric_imputation_values[col], inplace=True
            )
        for col in self.features_train.columns:
            if self.features_train[col].dtypes == "object":
                self.features_train[col].fillna(
                    self.categorical_imputation_values[col], inplace=True
                )
                self.features_eval[col].fillna(
                    self.categorical_imputation_values[col], inplace=True
                )
                self.features_test[col].fillna(
                    self.categorical_imputation_values[col], inplace=True
                )
        # Join features and target
        self.train = pd.concat([self.features_train, self.target_train], axis=1)
        self.eval = pd.concat([self.features_eval, self.target_eval], axis=1)
        self.test = pd.concat([self.features_test, self.target_test], axis=1)

        # Save preprocessed data to a file
        logging.info("Saving preprocessed data...")
        write_data(
            self.train,
            self.data_preprocessing_config["train_preprocessed_path"],
        )
        write_data(self.eval, self.data_preprocessing_config["eval_preprocessed_path"])
        write_data(self.test, self.data_preprocessing_config["test_preprocessed_path"])

```

E para finalizaar, a função final da classe DataPreprocessing será responsável por coordenar a execução de todo o processo do pré-processamento:

```python
    def initiate_data_preprocessing(self) -> None:
        """
        Initiates data preprocessing.
        Reads the data, splits it into features and target.
        Drops unnecessary columns.
        Replaces question marks with NaNs.
        Calculates imputation values and
        imputes missing values.
        Saves the preprocessed. The preprocessed data is saved
        to the files specified in the configuration file.
        The preprocessed data is saved as follows:
        - Train set: train_preprocessed_path
        - Eval set: eval_preprocessed_path
        - Test set: test_preprocessed_path
        Returns:
            pd.DataFrame: Preprocessed data.
        """
        try:
            self._split_into_features_and_target()
            self.drop_unnecessary_columns()
            self._replace_question_marks()
            self.calculate_imputation_values()
            self.impute_values()
        except Exception as e:
            raise ExceptionError(e)

```
