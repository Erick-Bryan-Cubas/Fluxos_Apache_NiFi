# Documentação sobre erro de falta de memória no Apache NiFi

## Problema

Ao executar um fluxo de dados no Apache NiFi, pode ocorrer o erro `java.lang.OutOfMemoryError: GC overhead limit exceeded`, indicando que o Garbage Collector está gastando muito tempo tentando liberar espaço na memória heap, sem sucesso.

## Causa

Esse erro ocorre quando um grande número de objetos é criado rapidamente, o que pode acontecer, por exemplo, quando um processador gera muitos objetos em um curto espaço de tempo.

## Solução

Uma solução para esse problema é aumentar o tamanho máximo do heap do NiFi. Isso pode ser feito no arquivo `bootstrap.conf`, modificando o valor da opção `-Xmx`. Por exemplo, você pode alterá-lo para `-Xmx4096m` para alocar 4 GB de memória heap. Após fazer essa alteração, é necessário reiniciar o NiFi e monitorar o uso de memória para verificar se o problema foi resolvido.

Se o problema persistir mesmo após aumentar o tamanho do heap, considere otimizar o fluxo de dados para reduzir a criação de objetos. Por exemplo, você pode dividir os arquivos em partes maiores, em vez de criar um FlowFile para cada linha do arquivo. Isso pode ser feito usando múltiplos processadores `SplitText` com diferentes limites de linhas.

## Exemplo de configuração do heap

```
# JVM memory settings
java.arg.2=-Xms8g
java.arg.3=-Xmx12g
```

Nesse exemplo, o tamanho da memória heap foi aumentado para 8 GB de memória inicial (`-Xms8g`) e 12 GB de memória máxima (`-Xmx12g`). Lembre-se de reiniciar o NiFi após fazer essa alteração no arquivo `bootstrap.conf`.

## Referências

- [StackOverflow](https://stackoverflow.com/questions/38653745/apache-nifi-outofmemory-error-gc-overhead-limit-exceeded-on-splittext-process)
- [Blog Archive](https://javarevisited.blogspot.com/2017/05/solution-of-javalangoutofmemoryerror-gc-overhead-limit-exceeded.html)