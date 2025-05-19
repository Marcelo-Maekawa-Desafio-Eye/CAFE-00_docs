# ![Café Ltda](https://raw.githubusercontent.com/Marcelo-Maekawa-Desafio-Eye/CAFE-00_docs/refs/heads/main/imagens_aux/logo04.png)


**Conteúdo**

**Conteúdo**

- [Visão Geral](#visão-geral) 
  - [Arquitetura](#arquitetura) 
  - [Infraestrutura](#infraestrutura)
  - [Estrutura de Repositórios](#estrutura-de-repositórios)
  - [Princípios de Desenvolvimento](#princípios-de-desenvolvimento)  
  - [Considerações Finais](#considerações-finais)  
- [Jornada do Usuário](#jornada-do-usuário)  
- [Requisitos de Sistema](#requisitos-de-sistema)  
  - [Requisitos Funcionais](#requisitos-funcionais)  
  - [Requisitos Não-Funcionais](#requisitos-não-funcionais)  
- [Arquitetura de Alto Nível](#arquitetura-de-alto-nível)  
  - [Design Patterns Utilizados](#design-patterns-utilizados)  
  - [Design de Dados](#design-de-dados)  
  - [ERD](#erd)  
  - [DDL](#ddl)  
- [Fatiamento das Tarefas e Sprints](#fatiamento-das-tarefas-e-sprints)  

## Visão Geral

Esse teste técnico consiste em uma aplicação fullstack que criará um canal de vendas para uma cafeteria. Após escanear um QRCode pré-fornecido,o usuário acessa o sistema pra exiber o cardápio, onde ele escolhe seus produtos, quantidades e faz personalizações, e, por fim, faz o pagamento e fechando o pedido.

Esse projeto segue a risca, uma série de "Requisitos de Negócio" bem definidos ([leia detalhes aqui](https://github.com/Marcelo-Maekawa-Desafio-Eye/CAFE-00_docs/tree/main/requisitos)). O objetivo da arquitetura proposta é demonstrar a aplicação de conceitos modernos e escaláveis, mesmo que, para um contexto de teste, isso possa parecer *overengineering*. A ideia foi aplicar ferramentas que garantam um sistema robusto e preparado para escalabilidade, mantendo um enfoque profissional e técnico.


## Fatiamento das tarefas e Sprints

## ✅ Sprint 0: Planejamento e Arquitetura (Concluído)  
- [x] Planejamento da arquitetura e escolha das tecnologias.  
- [x] Definição dos serviços e estrutura do projeto:  
  - Frontend (S3 + Cloudflare)  
  - BFF (EC2)  
  - API-Products (EC2)  
  - API-Orders (Lambda)  
  - Redis (ElastiCache)  
  - Banco de Dados (RDS MySQL)  
- [x] Escolha do stack tecnológico:  
  - NestJS, TypeScript, Redis, MySQL, Serverless Framework  
- [x] Documentação inicial:  
  - Arquitetura de alto nível e diagrama de sistema  
- [x] Fatiamento das tarefas e definição das sprints.  
- [x] Configuração inicial da infraestrutura no AWS e Cloudflare.  
- [x] Criação dos repositórios no GitHub:  
  - CAFE-01_frontend  
  - CAFE-02_bff  
  - CAFE-03_core-services  

---

## ✅ Sprint 1: Setup Inicial (Concluído)  
- [x] Configuração da AWS e Cloudflare.  
- [x] Criação do bucket S3 para o Frontend.  
- [x] Criação da VPC e Subnets privadas.  
- [x] Criação do RDS MySQL na VPC privada.  
- [x] Criação da instância EC2 para o BFF.  
- [x] Configuração do GitHub Actions para o Frontend.  

---

## ✅ Sprint 2: Desenvolvimento do Frontend (Concluído)  
- [x] Inicialização do projeto **Vite + React**.  
- [x] Configuração do CI/CD para o Frontend no GitHub Actions.  
- [x] Desenvolvimento da interface inicial e testes locais.  
- [x] Configuração do consumo do BFF para autenticação do usuário.  
- [x] Deploy do Frontend no S3 + Cloudflare.  

---

## ✅ Sprint 3: Desenvolvimento do BFF (Concluído)  
- [x] Inicialização do projeto **NestJS**.  
- [x] Configuração do CI/CD para o BFF no GitHub Actions.  
- [x] Desenvolvimento do módulo de autenticação (Login e JWT).  
- [x] Testes unitários da autenticação.  
- [x] Documentação com Swagger.  
- [x] Deploy no EC2 via GitHub Actions.  

---

## ✅ Sprint 4: Configuração do Redis (Concluído)  
- [x] Criação do Redis (Valkey) no ElastiCache.  
- [x] Atribuição do Security Group da VPC ao Redis.  
- [x] Teste de conexão entre o EC2 e o Redis.  
- [x] Teste de acesso direto ao Redis.  

---

## 🕐 Sprint 5: Configuração dos Lambdas e Core Services (Em Progresso)  
- [x] Criação do repositório **CAFE-03_core-services**.  
- [x] Inicialização do projeto com Serverless Framework.  
- [x] Configuração do Serverless para TypeScript.  
- [x] Desenvolvimento da função **updateMenu** para atualizar o Redis com dados do banco.  
- [x] Desenvolvimento da função **insertProducts** para popular o banco.  
- [ ] Criar o cron para disparar a atualização do Redis durante a madrugada.  
- [x] Configuração do **serverless.yml** para gerenciar múltiplas funções.  
- [x] Ajuste do CI/CD para deploy automático.  
- [ ] Criar token no Serverless Dashboard para deploy na v4.  
- [ ] Permitir acesso externo nas subnets privadas da VCP utilizada

---

## ✅ Sprint 6: Construção do Frontend e Finalização da Autenticação  
- [x] Implementar o consumo dos dados do cardápio diretamente do Redis.  
- [x] Ajustar o fluxo de autenticação no Frontend para usar o BFF.  
- [x] Testar o fluxo completo de login e consumo de dados.  

---

## 🕐 Sprint 7: Definição dos Últimos Endpoints no BFF e Criação dos Lambdas  
- [ ] Definir os endpoints finais do BFF para manipulação dos pedidos.  
- [ ] Criar as funções Lambda para obter os dados do banco de pedidos.  
- [ ] Configurar o BFF para acessar esses dados via Lambda.  

---

## 🕐 Sprint 8: Popular o Banco com Dados Fictícios  
- [ ] Criar um Lambda para inserir registros fake no banco.  
- [ ] Rodar o Lambda para popular o banco com dados de teste.  
- [ ] Verificar o preenchimento correto via consulta.  

---

## 🕐 Sprint 9: Teste de Integração e Consumo de Dados  
- [ ] Rodar o Lambda **insertProducts** para popular o banco.  
- [ ] Rodar o Lambda **updateMenu** para atualizar o Redis.  
- [ ] Configurar o BFF para consumir os dados diretamente do Redis.  
- [ ] Testar o fluxo completo (Frontend -> BFF -> Redis).  

---

## 🕐 Sprint 10: Testes Finais e Documentação  
- [ ] Testes de integração de ponta a ponta.  
- [ ] Testes de carga no BFF.  
- [ ] Documentação final do projeto, incluindo diagramas atualizados.  
- [ ] Checklist de boas práticas e padrões.  

---

## 🕐 Sprint 11: Finalização e Entrega  
- [ ] Revisão de todos os serviços e infraestrutura.  
- [ ] Verificação de segurança e boas práticas na AWS.  
- [ ] Apresentação e entrega formal do projeto.  



### Arquitetura

A solução proposta é composta por 3 componentes principais: **Frontend**, **BFF** e **Core Services**.

- **Frontend**: Interface que exibe o cardápio e permite ao usuário montar seu pedido e finalizar a compra.

- **BFF (Backend for Frontend)**: Centraliza a gestão de autenticação utilizando **JWT básico** e orquestra as chamadas às APIs, além de gerenciar regras de negócio. O BFF acessa o **Redis** para obter informações que mudam com baixa frequência (como dados do cardápio e produtos) e realiza chamadas às **APIs** presentes no **Core Services** para fechamento de pedidos e processamento do carrinho.

- **Core Services**: Um conjunto de FaaS (Functions as a Service) implementadas em **AWS Lambda**. Essas funções estão divididas em dois grupos principais:
  - **APIs**: Consumidas diretamente pelo BFF para operações de fechamento de pedidos e processamento do carrinho.
  - **Serviços Agendados**: Atualizam os valores no Redis a partir do **MySQL**, utilizando cron jobs na madrugada para minimizar impacto durante o uso.

### Infraestrutura

O sistema foi desenvolvido com foco em serviços de infraestrutura **gratuitos ou de baixo custo**. A escolha recaiu sobre a **AWS**, utilizando apenas serviços dentro do tier free, como **AWS Lambda** e **AWS RDS (MySQL)**. A gestão de DNS foi realizada pela **Cloudflare**, onde adquiri um domínio a custo reduzido, garantindo um ambiente profissional. A aplicação possui pipelines CI/CD automatizados utilizando **GitHub Actions**, com testes unitários e de integração, assegurando estabilidade e qualidade.

### Estrutura de Repositórios

Para manter a organização e o controle, a solução está estruturada em múltiplos repositórios:
- [**CAFE-00_docs** - *Documentação*](https://github.com/Marcelo-Maekawa-Desafio-Eye/CAFE-00_docs)
- [**CAFE-01_frontend** - *Frontend*](https://github.com/Marcelo-Maekawa-Desafio-Eye/CAFE-01_frontend)
- [**CAFE-02_bff** - *Backend for Frontend*](https://github.com/Marcelo-Maekawa-Desafio-Eye/CAFE-02_bff)
- [**CAFE-03_core-services** - *Core Services*](https://github.com/Marcelo-Maekawa-Desafio-Eye/CAFE-03_core-services)

Essa estrutura facilita o controle de versionamento e manutenção dos componentes, cada um configurado para rodar localmente usando **Docker Compose**.

### Princípios de Desenvolvimento

O projeto foi construído seguindo os princípios **DRY** e **SOLID**, aproveitando a modularidade proporcionada pelas FaaS para garantir responsabilidades bem definidas e facilitar a escalabilidade. O foco na modularização torna o sistema robusto e pronto para expansão, mesmo que seja apenas um teste técnico.

### Considerações Finais

Apesar da arquitetura ser um pouco mais complexa do que o necessário, a idéia foi considerar que o sistema deveria estar preparado para escalar, sem um aumento com o custo da infra, como também demonstrar boas práticas no uso de tecnologias modernas, equilibrando robustez, eficiência e escalabilidade.  A escolha por múltiplos serviços com CI/CD visa garantir um sistema que simula um cenário real de produção, mesmo que em um contexto de teste técnico.

## Jornada do Usuário

##### &nbsp;&nbsp;&nbsp;1. Acessa a **Interface** Inicial e **Principal** do sistema;
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&bull; *_No topo visualiza a logo e o nome do Usuário_*
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&bull; *_Na área central navega no cardápio_*
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&bull; *_No bloco à direita visualiza do pedido e finaliza a compra_*

2. Seleciona produtos na **Navegação do cardápio**;
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&bull; ~_Inicialmente visualiza a lista de categorias_~
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&bull; ~_Dentro da categoria exibe a lista de produtos_~
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&bull; ~_Dentro do produto exibe a info total_~
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&bull; *_Exibe TODOS os produtos e um bt comprar no hover (simplificando)_*

3. Edita ou Customiza a lista de produtos no **Carrinho**
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&bull; *_Em cada produto há uma  pequena foto e a descrição curta_*
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&bull; *_Abaixo da descrição temos um selecionador de quantidades (inicialmente sempre 01)_*
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&bull; *_Ao lado da quantidade um icone de uma lixeira para remoção da lista_*
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&bull; *_abaixo de tudo um campo de texto para observações livres_*

4. Visualiza o **Valor Total** da compra e clica em **Finalizar Pedido**
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&bull; *_Toda ação de adição, remoção ou mudança de quantidades atualiza o Total_*
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&bull; *_Abaixo existe um bt CTA que abre um modal de fechamento_*

5. Preenche os **Dados de Pagamento** 
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&bull; *_Pra retornar na edição do pedido, clica no bt cancelar_*
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&bull; *_Define o modo de pagamento (pra simplificar, permiti somente cartão de crédito)_*
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&bull; *_Preencher o formulário com dados do cartão_*
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&bull; *_Pra finalizar, clicar no botão "efetuar pagamento"_*
 
 6. Recebe feedback de **Confirmação**
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&bull; *_Aguarda visualizando um loader enquanto a transação é confirmada_*
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&bull; *_Recebe um aviso de Pedido Realizado_*
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&bull; *_Retorna à interface principal e pode assim, começar outro pedido_*


## Requisitos de Sistema

### Requisitos Funcionais

1. RF-01 - Inicialização da Sessão via QR Code  
O sistema deve permitir que o usuário inicie a sessão escaneando um QR Code, carregando a Interface Principal personalizada.

2. RF-02 - Exibição da Interface Principal  
Na tela principal o sistema deve mostrar:
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;- A logo "Café Ltda." no topo.
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;- O nome do usuário.
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;- O cardápio de produtos na área central.
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;- O resumo do carrinho e botão de finalização à direita.

3. RF-03 - Navegação e Seleção de Produtos  
Exibir todos os produtos do cardápio em uma lista única com botão "Comprar" visível ao passar o mouse (hover).

4. RF-04 - Gestão do Carrinho de Compras  
Permitir adicionar um produto ao carrinho ao clicar em "Comprar", e permitir para cada item no carrinho:
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;- Exibir foto em miniatura, descrição curta e seletor de quantidade (padrão = 1).
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;- Oferecer ícone de lixeira para remoção do item.
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;- Disponibilizar um campo de texto livre para observações do pedido.

5. RF-05 - Cálculo Dinâmico do Valor Total  
Recalcular e exibir o valor total sempre que um item for adicionado, removido ou alterada a quantidade.

6. RF-06 - Fluxo de Finalização de Pedido  
Ao clicar em "Finalizar Pedido", abrir um modal de confirmação.
Dentro do modal, oferecer botões "Cancelar" (fecha o modal) e "Prosseguir para Pagamento" (leva ao formulário).

7. RF-07 - Processamento de Pagamento com Cartão de Crédito  
Exibir formulário de pagamento com campos obrigatórios de cartão de crédito.
Validar dados do cartão (número, validade, CVV) em tempo real.
Enviar transação ao gateway e tratar retorno de sucesso ou erro.

8. RF-08 - Feedback de Confirmação  
Exibir loader enquanto a transação está em processamento.
Após aprovação, apresentar mensagem "Pedido Realizado" e retornar o usuário à Interface Principal pronta para novo pedido.

### Requisitos Não-Funcionais
1. RNF-01 - Desempenho  
A Interface Principal deve carregar em até 2 segundos em rede móvel 4G.
A adição/remoção de itens e o recálculo do total devem ocorrer em <500 ms.

2. RNF-02 - Disponibilidade  
O sistema deve manter 99,5 % de uptime mensal, com janelas de manutenção programadas fora do horário de pico.

3. RNF-03 - Segurança  
Toda comunicação deve usar HTTPS/TLS 1.2+.
Dados de cartão **não devem** ser armazenados no servidor (tokenização via gateway).
Seguir práticas de PCI-DSS para integração de pagamento.

4. RNF-04 - Usabilidade e Acessibilidade  
A UI deve ser responsiva para telas de smartphone (320 px a 1920 px).
Atender WCAG 2.1 nível AA para cores, contrastes e navegação por teclado.

5. RNF-05 - Escalabilidade  
A arquitetura deve suportar ao menos 200 pedidos simultâneos sem degradação perceptível.
Suportar adição horizontal de instâncias de aplicação e filas de processamento de pagamento.

6. RNF-06 - Manutenibilidade  
Código modularizado em front-end e back-end, com cobertura mínima de testes unitários de 80 %.
Documentação de API e instruções de deploy em repositório público.

## Arquitetura de Alto Nível
A arquitetura adotada para o projeto é híbrida, combinando serviços tradicionais hospedados em EC2 com funções serverless em AWS Lambda. Essa escolha permite manter a baixa latência para consultas ao cardápio, enquanto proporciona escalabilidade automática para operações de pedidos.

1. **Frontend (Cloudflare + Aws S3 - Vite + React.js)**: Interface do usuário para visualização do cardápio e realização de pedidos.

2. **Backend For Frontend (Aws EC2 - NestJS)**: Centraliza a orquestração das chamadas para as APIs e gestão de tokens JWT.

3. **API-Products (Aws EC2 - NestJS)**: Serviço contínuo que mantém o cardápio e realiza cache com Redis.

4. **API-Orders (Aws Lambda - Node.js)**: Função escalável para registro e consulta de pedidos.

5. **Banco de Dados (Aws RDS - MySQL)**: Armazenamento centralizado dos dados de produtos, pedidos e usuários.

6. **Cache (Aws ElastiCache - Redis)**: Armazenamento temporário para consultas rápidas do cardápio.

#### System Design Diagram
![System Design Diagram](https://raw.githubusercontent.com/Marcelo-Maekawa-Desafio-Eye/CAFE-00_docs/refs/heads/main/imagens_aux/system_design_diagram.png)
[Visualizar no Lucidcahrt parte 1](https://lucid.app/lucidchart/2c5f1769-1236-4fe2-8d54-05f026137335/edit?viewport_loc=5907%2C-112%2C3518%2C1343%2C0_0&invitationId=inv_1f9050f4-e9a1-4335-a4e5-d6d5b666094c) | [Visualizar no Lucidcahrt parte 2](https://lucid.app/lucidchart/b316f12c-e5b9-4f64-bb3a-0dc395906af7/edit?viewport_loc=-1906%2C1131%2C6131%2C4213%2C0_0&invitationId=inv_bf9ccd54-42d2-488c-b72b-aa272c173915)

### Definição de Padrões 
#### Padrão Arquitetural: Microserviços  
Cada módulo da aplicação é independente, facilitando o desenvolvimento, manutenção e escalabilidade.

#### Design Patterns Utilizados:
&nbsp;&nbsp;&nbsp;&nbsp;- **BFF (Backend for Frontend)**: Centraliza as chamadas do frontend para manter uma interface única.
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;- **Cache Aside**: O Redis armazena o cardápio e é atualizado quando o preço muda.
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;- **MVC (Model-View-Controller)**: Utilizado no BFF e nas APIs para separar responsabilidades.


 ## Design de Dados

 #### ERD
 ![ERD](https://raw.githubusercontent.com/Marcelo-Maekawa-Desafio-Eye/CAFE-00_docs/refs/heads/main/imagens_aux/cafe_er_diagram.png)

 [Visualizar no Lucidcahrt](https://lucid.app/lucidchart/83dd9643-6966-4f96-9f50-fa8f36951766/edit?viewport_loc=-868%2C45%2C3531%2C1348%2C0_0&invitationId=inv_b39a73b5-31b1-4218-b08e-97439baa18d6)

 #### DDL

 ```SQL
 CREATE DATABASE IF NOT EXISTS cafe;

USE cafe;

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(110) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    role ENUM('admin', 'saler', 'client') DEFAULT 'client',
    created TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE products (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(110) NOT NULL,
    description TEXT,
    price FIXED(10,2) UNSIGNED NOT NULL,
    image_url VARCHAR(255),
    created TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE orders (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    total_price FIXED(10,2) UNSIGNED,
    status ENUM('open', 'finished', 'canceled') DEFAULT 'open',
    created TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id)
);

CREATE TABLE order_items (
    id INT AUTO_INCREMENT PRIMARY KEY,
    order_id INT,
    product_id INT,
    quantity INT,
    price FIXED(10,2) UNSIGNED,
    FOREIGN KEY (order_id) REFERENCES orders(id) ON DELETE CASCADE,
    FOREIGN KEY (product_id) REFERENCES products(id)
);

CREATE TABLE payments (
    id INT AUTO_INCREMENT PRIMARY KEY,
    order_id INT,
    amount FIXED(10,2) UNSIGNED,
    method ENUM('credit', 'pix', 'cash'),
    transaction_id VARCHAR(100) DEFAULT NULL,
    gateway_response TEXT,
    status ENUM('open', 'paid', 'fail') DEFAULT 'open',
    created TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (order_id) REFERENCES orders(id)
);
```
