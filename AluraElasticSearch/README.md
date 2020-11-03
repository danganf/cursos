# [Elasticsearch: Executando buscas inteligentes](https://cursos.alura.com.br/course/elasticsearch-introducao)
## Instalação
* CURL
    * executar o seguinte comando no powershell
```sh
choco install curl --version 7.73.0  
```
* JVM
    * ter JVM instalado na máquina
* [ElasticSearch 7.4.2](https://www.elastic.co/pt/downloads/past-releases/elasticsearch-7-4-2)
* [Kibana 7.4.2](https://www.elastic.co/pt/downloads/past-releases/kibana-7-4-2)

## Inicialização
* executar `kibana-7.4.2-windows-x86_64\bin\kibana.bat`
    * testar fazendo um GET em `http://localhost:5601/`
* executar `elasticsearch-7.4.2\bin\elasticsearch.bat`
    * testar fazendo um GET em `http://localhost:9200/`
***
## Aula 1
* O que é e para que serve o ElasticSearch.
* Como fazer uma instalação básica do ElasticSeach a ser usada em uma única máquina.
* Como instalar o Kibana e o cURL.
* Como utilizar um cliente REST para criar e localizar documentos por identificador, listar todos os documentos ou aplicar um valor simples para consulta.

## Aula 2
* O que é um índice, tipo e documento.
* Como utilizar a API Rest para operações de criação, atualização, remoção e verificação de existência de documentos no ElasticSearch.
* A analogia entre ElasticSearch e um banco de dados relacionais.
* O que são shards, réplicas e qual a sua importância.

## Aula 3
* Que podemos especificar o campo na busca usando `campo:termo`.
* ElasticSearch retorna 10 resultados por padrão.
* A entender as estatísticas que são parte da resposta de requisições de busca, como tempo de resposta e hits.