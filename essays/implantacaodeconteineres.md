---
layout: essay
type: essay
title: MLOps - Implantação de Contêineres
# All dates must be YYYY-MM-DD format!
date: 2023-09-04
labels:
  - Machine Learning Engineer
  - MLOps
  - Aprender ensinando
---

Em MLOps, a implantação eficiente de modelos de Machine LEarning é essencial. Uma das ferramentas com maior destaque nesse cenário é o Docker. Vamos explorar como o Docker pode resolver problemas comuns na implantação de modelos de ML, incluindo como ele funciona tecnicamente e como podemos aproveita-lo para melhorar nossas práticas de MLOps.

## O que é um Container Docker?
É fundamental entender o que é um container Docker tecnicamente. Um container é construído a partir de imagens, formando camadas empilhadas umas sobre as outras. Na base da maioria dos containers, você encontrará uma imagem base de Linux, geralmente Alpine com uma versão específica ou outra distribuição Linux semelhante. Essas imagens base precisam ser pequenas para garantir que os containers permaneçam com o tamanho reduzido, um dos principais benefícios de sua utilização.

Em cima da imagem base, você terá uma imagem de aplicativo, que no contexto de MLOps, pode conter seu modelo de Machine Learning e todas as suas bibliotecas e dependências necessárias. Isso cria uma unidade portátil e isolada, pronta para ser compartilhada e executada em qualquer ambiente.

## Exemplo de uso de um Container Docker para MLOps

Pensando em um modelo hipotético, que usa a combinação de Python e TensorFlow, e precisa ser implentado em produção. Para garantir que o modelo funcione consistentemente em todas as etaps, desde o desenvolvimento até o deploy em produção, você pode empacotá-lo em um container Docker.

Primeiro será necessário criar a imagem Docker, que inclui o modelo, juntamente com suas bibliotecas e dependências. Essa imagem será a base para a implantação do modelo.

```bash
# Dockerfile
# Selecionando uma imagem base com python 3.8 em sua versão slim, que a torna bem mais compacta
FROM python:3.8-slim

# Copie o código do modelo da maquina para o container
COPY model.py /app/

# Instale as dependências, aqui instalamos diretamente mas o usual seria por meio do requirements.txt
RUN pip install tensorflow scikit-learn

# Defina o comando de entrada, esse comando será executado quando a image estiver em execução
CMD ["python", "/app/model.py"]
```

Em seguida copilamos (construímos) a imagem:

```
docker build -t meu-modelo:1.0 .
```

Basicamente indicamos a receita e em seguida executamos a receita, com a imagem gerada agora podemos de fato colocar ela para funcionar:

```
docker run meu-modelo:1.0
```

Isso garante que o modelo será executado com as mesmas configurações e dependências em todas as etapas do pipeline de MLOps, desde o desenvolvimento até a produção.

## Benefícios

O uso de Docker oferece diversos benefícios:

1. **Isolamento e Portabilidade:** O modelo de ML e suas dependências estão encapsulados em um container, garantindo que eles funcionem consistentemente em diferentes ambientes, evitando problemas de "na minha máquina funciona"
2. **Implantação Eficiente:** Com o Docker, é possivel implantar modelos rapidamente, sem a necessidade de configurar manualmente as dependências em cada ambiente
3. **Versões e Consistência:** Você pode gerenciar diferentes versões de seus modelos de ML usando containers separados, garantindo consistência e facilitando atualizações.
4. **Colaboração:** Equipes podem compartilhar os modelos facilmente, permitindo uma colaboração eficaz durante o desenvolvimento do modelo.

O Docker se tornou uma ferramenta valiosa no ecossistema de Machine Learning, tornando a implantação dos modelos mais eficiente e consistente em todas as etapas do processo completo, sendo uma ferramenta perfeitamente alinhada com as melhores práticas de MLOps.


Além do canal da [LinuxTips](https://www.youtube.com/@LinuxTips), que eu considero a melhor fonte brasileira de DevOps, também indico os artigos da [techworld-with-nana](https://www.techworld-with-nana.com/blog/categories/docker-tutorials), outra grande fonte de conhecimento. Ambos foram a base do meu aprendizado sobre Docker.
