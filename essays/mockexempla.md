---
layout: essay
type: essay
title: MagicMock Example
# All dates must be YYYY-MM-DD format!
date: 2023-11-20
labels:
  - Example
  - unit test
  - Mocks
---

```python
# funcoes.py


def contar_linhas_arquivo(nome_arquivo):
    with open(nome_arquivo, "r") as arquivo:
        linhas = arquivo.readlines()
    return len(linhas)

```

```python
# test_funcoes.py
import io
import unittest
from unittest.mock import MagicMock, patch

from funcoes import contar_linhas_arquivo


class TestContarLinhasArquivo(unittest.TestCase):
    @patch("funcoes.open", create=True)
    def test_contar_linhas_arquivo(self, mock_open):
        # Configurar o MagicMock para retornar um objeto de arquivo falso em memória
        mock_arquivo = MagicMock()
        mock_arquivo.__enter__.return_value = io.StringIO("Linha 1\nLinha 2\nLinha 3")
        mock_open.return_value = mock_arquivo

        # Chamar a função que estamos testando
        num_linhas = contar_linhas_arquivo("arquivo_ficticio.txt")

        # Verificar se a função open foi chamada com o nome do arquivo correto
        mock_open.assert_called_once_with("arquivo_ficticio.txt", "r")

        # Verificar se a função retornou o número correto de linhas
        self.assertEqual(num_linhas, 3)


if __name__ == "__main__":
    unittest.main()

```

1. '@patch('funcoes.open', create=True): Esta linha usa o decorador @patch para substituir a função open no módulo funcoes por um objeto mock. O argumento create=True indica que, se a função open não existir no momento em que o patch é aplicado, ela será criada como um objeto mock.

2. mock_arquivo = MagicMock(): Aqui, estamos criando um objeto mock chamado mock_arquivo. Esse objeto será usado para simular um arquivo em memória.

3. mock_arquivo.__enter__.return_value = io.StringIO("Linha 1\nLinha 2\nLinha 3"): Os objetos de arquivo em Python podem ser usados como gerenciadores de contexto usando o método __enter__. Para simular esse comportamento, estamos configurando o atributo return_value do __enter__ do nosso mock para retornar um objeto io.StringIO. io.StringIO é uma classe que permite criar um arquivo em memória com um conteúdo específico. Neste caso, estamos criando um arquivo em memória com três linhas fictícias.

4. mock_open.return_value = mock_arquivo: Esta linha define o retorno do nosso mock da função open. O mock_open agora retorna o mock_arquivo quando é chamado, simulando com sucesso a abertura de um arquivo.

Portanto, quando a função contar_linhas_arquivo é chamada no teste, ela utiliza open("arquivo_ficticio.txt", "r"), mas o open foi substituído pelo mock_open, que retorna o mock_arquivo. O mock_arquivo age como um arquivo em memória contendo as linhas fictícias, permitindo que o teste seja executado sem depender de um arquivo real no sistema de arquivos.

Em resumo, este código usa mocks para simular a abertura de um arquivo e permite que você forneça dados fictícios para a função contar_linhas_arquivo, tornando o teste independente de arquivos reais.
