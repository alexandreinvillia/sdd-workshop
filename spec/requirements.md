# Requisitos do Sistema de Pedidos

## Objetivo
Definir as regras principais para um sistema de pedidos que permita cadastrar clientes, produtos e processar pedidos com controle de status.

## Escopo
O sistema deve permitir:
- Cadastro e consulta de clientes
- Cadastro e consulta de produtos
- Criacao de pedidos com multiplos itens
- Calculo de subtotal, descontos, frete e total
- Atualizacao e rastreio do status do pedido
- Registro de pagamento e confirmacao

## Entidades Principais

### Cliente
- id (unico, obrigatorio)
- nome (obrigatorio)
- email (obrigatorio, unico, formato valido)
- telefone (opcional)
- endereco de entrega padrao (opcional)

### Produto
- id (unico, obrigatorio)
- nome (obrigatorio)
- sku (unico, obrigatorio)
- preco (obrigatorio, maior que zero)
- estoque (obrigatorio, inteiro maior ou igual a zero)
- ativo (obrigatorio, booleano)

### Pedido
- id (unico, obrigatorio)
- cliente_id (obrigatorio)
- data_criacao (obrigatorio)
- status (obrigatorio)
- itens (um ou mais)
- subtotal (obrigatorio)
- desconto (padrao zero)
- frete (padrao zero)
- total (obrigatorio)
- forma_pagamento (opcional ate confirmacao)
- status_pagamento (obrigatorio apos tentativa de pagamento)

### Item do Pedido
- pedido_id (obrigatorio)
- produto_id (obrigatorio)
- quantidade (obrigatorio, inteiro maior que zero)
- preco_unitario (obrigatorio, maior que zero)
- total_item (obrigatorio)

## Regras de Negocio

### Criacao de Pedido
- Um pedido deve estar vinculado a um cliente existente.
- Um pedido deve ter pelo menos 1 item.
- Nao deve ser permitido adicionar produto inativo ao pedido.
- Nao deve ser permitido adicionar item com quantidade maior que o estoque disponivel.
- O preco_unitario do item deve ser capturado no momento da criacao do pedido.

### Calculos
- total_item = quantidade * preco_unitario
- subtotal = soma(total_item de todos os itens)
- total = subtotal - desconto + frete
- O total final nao pode ser negativo.

### Estoque
- Ao confirmar pedido, o estoque deve ser reservado ou baixado.
- Ao cancelar pedido confirmado, o estoque deve ser devolvido.
- O sistema deve impedir estoque negativo.

### Status do Pedido
Status permitidos:
- CRIADO
- AGUARDANDO_PAGAMENTO
- PAGO
- EM_SEPARACAO
- ENVIADO
- ENTREGUE
- CANCELADO

Transicoes validas:
- CRIADO -> AGUARDANDO_PAGAMENTO
- AGUARDANDO_PAGAMENTO -> PAGO
- AGUARDANDO_PAGAMENTO -> CANCELADO
- PAGO -> EM_SEPARACAO
- EM_SEPARACAO -> ENVIADO
- ENVIADO -> ENTREGUE
- CRIADO -> CANCELADO
- PAGO -> CANCELADO (somente com estorno)

Regras:
- Nao permitir transicoes fora do fluxo definido.
- Pedido CANCELADO nao pode voltar para status ativo.
- Pedido ENTREGUE nao pode ser cancelado.

### Pagamento
- Formas permitidas: CARTAO, PIX, BOLETO.
- Status de pagamento: PENDENTE, APROVADO, RECUSADO, ESTORNADO.
- Somente pedidos com pagamento APROVADO podem seguir para EM_SEPARACAO.
- Em cancelamento de pedido pago, deve haver registro de estorno quando aplicavel.

### Descontos e Frete
- Desconto percentual deve estar entre 0 e 100.
- Desconto em valor nao pode exceder o subtotal.
- Frete deve ser maior ou igual a zero.
- Todas as alteracoes de desconto e frete devem ser auditaveis.

## Requisitos Funcionais
- RF01: Cadastrar, editar e consultar clientes.
- RF02: Cadastrar, editar e consultar produtos.
- RF03: Criar pedido com um ou mais itens.
- RF04: Recalcular subtotal e total automaticamente ao alterar itens.
- RF05: Atualizar status do pedido respeitando transicoes validas.
- RF06: Registrar tentativa e resultado de pagamento.
- RF07: Cancelar pedido conforme regras de status e pagamento.
- RF08: Consultar historico de alteracoes do pedido.

## Requisitos Nao Funcionais
- RNF01: Validar dados de entrada antes de persistir.
- RNF02: Garantir consistencia transacional em operacoes de pedido e estoque.
- RNF03: Registrar logs de auditoria para mudancas de status e valores.
- RNF04: Retornar mensagens de erro claras em violacoes de regra.
- RNF05: Permitir rastreabilidade por id de pedido, cliente e produto.

## Criterios de Aceite (exemplos)
- CA01: Pedido com item sem estoque suficiente deve ser rejeitado com erro explicito.
- CA02: Pedido sem itens nao deve ser salvo.
- CA03: Pedido pago deve permitir avancar para EM_SEPARACAO.
- CA04: Pedido cancelado deve bloquear novas transicoes.
- CA05: Total calculado deve refletir corretamente itens, desconto e frete.
