# Erro: "Unable to write flowfile content to content repository container default due to archive file size constraints; waiting for archive cleanup."

Data: 14 de junho de 2023

O problema foi encontrado no Apache NiFi, onde a aplicação apresentava uma mensagem de erro informando que não era capaz de gravar o conteúdo do FlowFile no repositório devido a restrições de tamanho do arquivo de arquivamento.

## Problema

O Apache NiFi é uma ferramenta poderosa para automação de fluxo de dados. Durante uma operação, surgiu a seguinte mensagem de erro:

```plaintext
2023-06-14 11:02:54,604 WARN [Timer-Driven Process Thread-5] o.a.n.c.repository.FileSystemRepository Unable to write flowfile content to content repository container default due to archive file size constraints; waiting for archive cleanup. Total number of files currently archived = 13
```

Essa mensagem indica que o NiFi não conseguia escrever o conteúdo do FlowFile no repositório devido a restrições de tamanho do arquivo de arquivamento.

## Solução

A solução encontrada foi aumentar a porcentagem de uso máximo permitido para o arquivo de arquivamento. Isso foi feito modificando o arquivo `nifi.properties` localizado no diretório `conf` da instalação do Apache NiFi. A configuração alterada foi `nifi.content.repository.archive.max.usage.percentage`, que foi ajustada de 50% para 75%. 

O ajuste na configuração é mostrado a seguir:

```plaintext
# Antes da alteração
nifi.content.repository.archive.max.usage.percentage=50%

# Depois da alteração
nifi.content.repository.archive.max.usage.percentage=75%
```

Após fazer a alteração, o serviço do Apache NiFi foi reiniciado e o erro foi resolvido.

## Conclusão

O ajuste de configurações em ferramentas complexas como o Apache NiFi deve ser realizado com cuidado. Ajustes como o realizado aqui podem ter impacto significativo no funcionamento da ferramenta e no uso de recursos do sistema. Recomenda-se sempre monitorar de perto o sistema após fazer alterações como essa.

Este documento foi preparado com a ajuda de ChatGPT, a IA de linguagem natural da OpenAI. 

Créditos: ChatGPT, OpenAI
