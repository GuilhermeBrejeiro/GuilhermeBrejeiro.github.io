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

## Engenharia de Recursos
A engenharia de recursos, também conhecida como feature engineering, desempenha um papel crucial na construção de modelos de aprendizado de máquinas. Nesta seção, vou explorar algumas técnicas muito utilizadas para transformar os recursos de entrada brutos e aprimorar o desempenho do modelo de previsão de aprovações de cartões de crédito.

Como feito anteriormente, iniciamos o processo com as configurações já pré-definidas, que estão em um arquivo separado e devem ser importadas:

```python
from configs.project_config import FeatureEngineeringConfig
```
A classe 'FeatureEngineeringConfig' do arquivo de configurações 'project_config.py'contém as configurações necessárias para a engenharia de recursos:

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

O arquivo 'feature_engineering.py'contém a classe 'FeatureEngineering' com as funções responsáveis pela engenharia de recursos. Abaixo as definições de inicialização da classe e, nesse arquivo especifico, como foram declaradas uma imensa quantidade de váriaveis iniciais, uma boa prática é separa-las e organiza-las, para isso utilizamos um decorator chamado 'dataclass'
