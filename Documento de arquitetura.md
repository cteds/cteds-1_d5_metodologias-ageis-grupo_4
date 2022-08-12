# 1 Introdução
## 1.1 Objetivo
Este documento mostra uma visão geral da arquitetura do sistema.

## 1.2 Escopo
Este documento se refere ao projeto FipeD5, um sistema que permite ao usuário realizar pesquisas de dados da Tabela Fipe de veículos em massa. O projeto foi realizado para a disciplina D5 - Metodologias Ágeis do curso CTEDS, 1º oferecimento.

# 2 Representação Arquitetural
## 2.1 Banco de dados em MySQL
O banco de dados será responsável por armazenar as informações obtidas nas consultas com os crawlers, permitindo que os dados possam ser consultados posteriormente na plataforma.
Além disso, o banco de dados armazenará informações de cadastro do usuário, de empresas e de veículos por ele adicionados para consulta.

## 2.2 Back-end em C#
### 2.2.1 Interação do crawler com o banco de dados
O back-end é responsável pela interação do crawler com o banco de dados.
Assim que uma consulta é realizada, os dados serão salvos no banco de dados, atrelada ao veículo, à empresa e ao usuário responsável.

### 2.2.2 Interação da plataforma com o banco de dados
Além disso, o back-end também é responsável pela inserção de cadastro no banco de dados, autenticação, de usuários, criação de empresa, adição de veículos para consulta, visualização da lista de veículos e visualização de detalhes de veículos.

## 2.3 Crawler em node.js
O crawler será feito em node js, com o uso da biblioteca puppeteer, que permite automatizar ações em uma página web e extrair as informações desejadas. Assim, o crawler receberá as informações do veículo, obterá as informações da página web e utilizará o back-end em C# para salvar as informações no banco de dados.

## 2.4 Gerenciamento de mensagens
### 2.4.1 Filas
Os veículos adicionados na plataforma serão enviados a uma fila, de modo a permitir um processamento assíncrono para não sobrecarregar a página de onde vem os dados a serem obtidos.
### 2.4.2 Consumidor
O consumidor se trata de uma aplicação gerenciada pelo pm2, um gestor de processos para node.js que permite escalar o número de processos de crawler sendo executados simultaneamente. Assim, sempre que houver uma mensagem na fila, um dos processos de crawler assumirá a mensagem e realizará o seu processamento. 

# 3 Referências
- [PM2](https://pm2.keymetrics.io/docs/usage/quick-start/)
- [Puppeteer](https://devdocs.io/puppeteer/)
