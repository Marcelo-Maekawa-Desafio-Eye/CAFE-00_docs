# ![Café Ltda.][imagens_aux/logo04.png]

###### conteúdo:

## Visão Geral 

Esse teste técnico consiste em uma aplicação fullstack que criará um canal de vendas para uma cafeteria.  
Esse projeto contém uma série de "Requisitos de Negócio" bem definidos (leia aqui), mas, basicamente, o cliente, após fazer login no sistema, acessa a interface para realizar e personalizar o seu pedido, finalizando-o após o pagamento.  

A minha solução para esse teste será composta por 4 peças-chave: **Frontend**, **BFF**, **API-Produtos** e **API-Pedidos**.  
Apesar de haver um certo nível de *overengineering* nessa arquitetura, por se tratar de um teste no formato de desafio, acredito que, desse modo, consigo exibir um resultado ao mesmo tempo **tecnicamente complexo**, mas que não pode ser acusado de uso **inadequado de ferramentas**.  

O BFF existe para centralizar a gestão de tokens e gerenciar as chamadas para as diferentes APIs. Além disso, o BFF também será responsável pela **gestão do cache Redis**, realizando operações de **Cache Invalidation** e **Cache Refresh** para garantir que os dados do cardápio estejam sempre atualizados e sincronizados com o banco de dados.  

A escolha por uma arquitetura híbrida entre **EC2 e Lambda** se justifica pela necessidade de manter um serviço contínuo para o cardápio (produtos), garantindo **baixa latência e alta disponibilidade**, enquanto o uso de **FaaS para pedidos** permite escalabilidade automática para lidar com picos de demanda.  

Para garantir a **consistência histórica**, o preço de cada item é armazenado diretamente na tabela de pedidos no momento da compra. Dessa forma, mesmo que o valor do produto mude posteriormente, os registros antigos permanecem corretos, preservando a integridade financeira dos relatórios.  

A aplicação será configurada com **pipelines CI/CD automatizados** utilizando **GitHub Actions**, garantindo que novas atualizações passem por testes e validações antes do deploy, mantendo a qualidade e a estabilidade do sistema.  

Dessa forma, a arquitetura que proponho para o desafio, busca equilibrar complexidade e eficiência, garantindo um sistema robusto e escalável.

## Jornada do Usuário

1. Acessa a **Interface** Inicial e **Principal** do sistema;
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
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&bull; *_se quiser retornar à edição do pedido, clica no bt cancelar_*
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&bull; *_seleção de modos de pagamento somente com o cartão de credito como ativo (simplificando)_*
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&bull; *_preenche formulário com os dados do modo de pagamento_*
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&bull; *_clica no botão "efetuar pagamento"_*

6. Recebe feedback de **Confirmação**
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&bull; *_Aguarda visualizando um loader enquanto a transação é confirmada_*
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&bull; *_Recebe um aviso de Pedido Realizado_*
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&bull; *_Retorna à interface principal e pode assim, começar outro pedido_*


## Requisitos de Sistema

### Requisitos Funcionais

1. RF-01 – Inicialização da Sessão via QR Code  
O sistema deve permitir que o usuário inicie a sessão escaneando um QR Code, carregando a Interface Principal personalizada.

2. RF-02 – Exibição da Interface Principal  
Na tela principal o sistema deve mostrar:
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;- A logo “Café Ltda.” no topo.
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;- O nome do usuário autenticado.
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;- O cardápio de produtos no centro.
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;- O resumo do carrinho e botão de finalização à direita.

3. RF-03 – Navegação e Seleção de Produtos  
Exibir todos os produtos do cardápio em uma lista única com botão “Comprar” visível ao passar o mouse (hover).

4. RF-04 – Gestão do Carrinho de Compras  
Permitir adicionar um produto ao carrinho ao clicar em “Comprar”, e permitir para cada item no carrinho:
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;- Exibir foto em miniatura, descrição curta e seletor de quantidade (padrão = 1).
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;- Oferecer ícone de lixeira para remoção do item.
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;- Disponibilizar um campo de texto livre para observações do pedido.

5. RF-05 – Cálculo Dinâmico do Valor Total  
Recalcular e exibir o valor total sempre que um item for adicionado, removido ou alterada a quantidade.

6. RF-06 – Fluxo de Finalização de Pedido  
Ao clicar em “Finalizar Pedido”, abrir um modal de confirmação.
Dentro do modal, oferecer botões “Cancelar” (fecha o modal) e “Prosseguir para Pagamento” (leva ao formulário).

7. RF-07 – Processamento de Pagamento com Cartão de Crédito  
Exibir formulário de pagamento com campos obrigatórios de cartão de crédito.
Validar dados do cartão (número, validade, CVV) em tempo real.
Enviar transação ao gateway e tratar retorno de sucesso ou erro.

8. RF-08 – Feedback de Confirmação  
Exibir loader enquanto a transação está em processamento.
Após aprovação, apresentar mensagem “Pedido Realizado” e retornar o usuário à Interface Principal pronta para novo pedido.

### Requisitos Não-Funcionais
1. RNF-01 – Desempenho  
A Interface Principal deve carregar em até 2 segundos em rede móvel 4G.
A adição/remoção de itens e o recálculo do total devem ocorrer em <500 ms.

2. RNF-02 – Disponibilidade  
O sistema deve manter 99,5 % de uptime mensal, com janelas de manutenção programadas fora do horário de pico.

3. RNF-03 – Segurança  
Toda comunicação deve usar HTTPS/TLS 1.2+.
Dados de cartão **não devem** ser armazenados no servidor (tokenização via gateway).
Seguir práticas de PCI-DSS para integração de pagamento.

4. RNF-04 – Usabilidade e Acessibilidade  
A UI deve ser responsiva para telas de smartphone (320 px a 1920 px).
Atender WCAG 2.1 nível AA para cores, contrastes e navegação por teclado.

5. RNF-05 – Escalabilidade  
A arquitetura deve suportar ao menos 200 pedidos simultâneos sem degradação perceptível.
Suportar adição horizontal de instâncias de aplicação e filas de processamento de pagamento.

6. RNF-06 – Manutenibilidade  
Código modularizado em front-end e back-end, com cobertura mínima de testes unitários de 80 %.
Documentação de API e instruções de deploy em repositório público.

## Arquitetura de Alto Nível
A arquitetura adotada para o projeto é híbrida, combinando serviços tradicionais hospedados em EC2 com funções serverless em AWS Lambda. Essa escolha permite manter a baixa latência para consultas ao cardápio, enquanto proporciona escalabilidade automática para operações de pedidos.

1. **Frontend (CloudFront - React.js)**: Interface do usuário para visualização do cardápio e realização de pedidos.

2. **Backend For Frontend (EC2 - NestJS)**: Centraliza a orquestração das chamadas para as APIs e gestão de tokens JWT.

3. **API-Produtos (EC2 - NestJS)**: Serviço contínuo que mantém o cardápio e realiza cache com Redis.

4. **API-Pedidos (Lambda - Node.js)**: Função escalável para registro e consulta de pedidos.

5. **Banco de Dados (RDS - MySQL)**: Armazenamento centralizado dos dados de produtos, pedidos e usuários.

6. **Cache (ElastiCache - Redis)**: Armazenamento temporário para consultas rápidas do cardápio.

## Definição de Padrões 
#### Padrão Arquitetural: Microserviços  
Cada módulo da aplicação é independente, facilitando o desenvolvimento, manutenção e escalabilidade.

#### Design Patterns Utilizados:
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;- **BFF (Backend for Frontend)**: Centraliza as chamadas do frontend para manter uma interface única.
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;- **Cache Aside**: O Redis armazena o cardápio e é atualizado quando o preço muda.
 <br /> &nbsp;&nbsp;&nbsp;&nbsp;- **MVC (Model-View-Controller)**: Utilizado no BFF e nas APIs para separar responsabilidades.