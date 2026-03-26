# Avaliação — Engenharia de Software
**Sistema Integrado de Gestão de Farmácia — MVP Definido pelo Estudante**

Aluno: *Henrique de Oliveira Molinari*
RA: *25001176*
Data: *25/03/2026*

---

# 1. Definição do MVP

O MVP pensado por mim cobre o ciclo operacional principal de uma farmácia, partindo desde o atendimento ao cliente (balcão) até na parte financeira das operações. O maior foco está nos processos, pois se não funcionarem, travam o funcionamento básico da empresa.

**Dentro do MVP:**
- Cadastro e consulta de produtos
- Cadastro e consulta de clientes (com histórico de compras)
- Realização de vendas (a vista e a prazo)
- Emissão de comprovante com detalhes da operação de venda
- Controle e atualização de estoque (atualizado automaticamente após venda, devolução, perda, compra etc.)
- Registro de compras de fornecedores (com atualização automática de estoque)
- Lançamento automático de contas a receber e contas a pagar (para convênios e operações internas das unidades)
- Consulta rápida de lançamentos financeiros (abertos, atrasados e pagos)
- Alerta de estoque mínimo
- Geração de relatórios simples de indicadores (top produtos mais vendidos, estoque por unidade, vendas por período)
- Separação de perfis e permissões por função (Atendente, Farmacêutico, Gerente, Financeiro e Administrador)

**Fora do MVP:**
- Emissão de nota fiscal eletrônica (NF-e)
- Transferência de estoque entre unidades
- Dashboards e relatórios gerenciais avançados
- Aplicativo mobile
- Integração com planos de saúde e convênios externos

**Justificativa**
O foco foi garantir que o ciclo básico da farmácia funcionasse: atender o cliente, registrar a venda, controlar o estoque e refletir tudo no financeiro. A geração de relatórios simples também foi incluída, pois mesmo num MVP os gestores precisam de alguma visibilidade para tomar decisões no dia a dia. O que ficou de fora não trava a operação e pode entrar numa próxima versão. Essa delimitação permite entregar algo funcional e testável mais rápido, com base para crescer.

---

# 2. Regras de Negócio

**RN01 — Venda somente com estoque disponível**
Nenhuma venda pode ser finalizada se a quantidade solicitada pelo cliente for maior que o saldo em estoque da unidade no momento do atendimento. O sistema deve bloquear a operação e informar o saldo atual.

**RN02 — Receita obrigatória para medicamentos controlados**
Medicamentos com controle especial só podem ser vendidos após a validação e registro da receita médica por um farmacêutico. Sem essa etapa, a venda não pode ser concluída.

**RN03 — Atualização automática de estoque**
Toda movimentação, venda, devolução, compra ou registro de perda, deve refletir imediatamente no saldo de estoque da unidade responsável pela operação, sem necessidade de atualização manual.

**RN04 — Venda a prazo gera lançamento em contas a receber**
Quando uma venda for registrada com forma de pagamento a prazo, o sistema deve criar automaticamente um lançamento em contas a receber com valor, data de vencimento e status inicial "Aberta".

**RN05 — Compra gera lançamento em contas a pagar**
AS compras registradas junto a um fornecedor devem gerar automaticamente um lançamento em contas a pagar, com o valor total da compra, data de vencimento acordada e status inicial "Aberta".

**RN06 — Alerta de estoque mínimo**
Quando o saldo de um produto atingir ou ficar abaixo do nível mínimo estipulado, o sistema deve emitir um alerta ao gerente, sem bloquear as demais operações.

**RN07 — Acesso restrito por perfil**
Cada funcionalidade do sistema é acessível apenas pelo perfil autorizado. Um atendente, por exemplo, não pode cadastrar novos produtos nem acessar lançamentos financeiros. As permissões devem ser definidas pelo usuario administrador.

---

# 3. Requisitos Funcionais

**RF01 — Cadastrar e consultar clientes**
O sistema deve permitir o registro de novos clientes com o nome, CPF, contato e endereço, além de possibilitar a consulta de clientes já cadastrados durante o atendimento e o acesso ao histórico de compras do mesmo.

**RF02 — Cadastrar e consultar produtos**
O sistema deve permitir o cadastro de produtos com descrição, código de barras, preço e fabricante. Além de possibilitar buscas por nome, código ou fabricante.

**RF03 — Realizar venda**
O sistema deve permitir ao atendente registrar uma venda, selecionando o cliente, os produtos e quantidades, verificando automaticamente o estoque, calculando o total e finalizando com a emissão do comprovante.

**RF04 — Registrar venda a prazo**
O sistema deve suportar a finalização de vendas com pagamento a prazo, gerando automaticamente o lançamento correspondente em contas a receber.

**RF05 — Controlar estoque por unidade**
O sistema deve manter o saldo atualizado de cada produto por unidade, refletindo automaticamente qualquer movimentação registrada.

**RF06 — Registrar compra de fornecedor**
O sistema deve permitir o lançamento de compras, informando fornecedor, produtos, quantidades, valores e a data, atualizando o estoque e gerando o lançamento em contas a pagar.

**RF07 — Gerenciar contas a pagar**
O sistema deve listar, filtrar e atualizar lançamentos de contas a pagar, permitindo registrar pagamentos e acompanhar os status (Aberta, Paga, Atrasada).

**RF08 — Gerenciar contas a receber**
O sistema deve listar, filtrar e atualizar lançamentos de contas a receber, permitindo registrar recebimentos e acompanhar os status (Aberta, Recebida, Atrasada).

**RF09 — Emitir alerta de estoque mínimo**
O sistema deve identificar os produtos com saldo igual ou menor ao mínimo estipulado e exibir alertas ao gerente da unidade.

**RF10 — Controle de acesso por perfil**
O sistema deve autenticar usuários e restringir o acesso às funcionalidades conforme o perfil atribuído (Atendente, Farmacêutico, Gerente, Financeiro, Administrador).

**RF11 — Gerar relatórios simples de indicadores**
O sistema deve permitir a geração de relatórios básicos como produtos mais vendidos, saldo de estoque por unidade e total de vendas por período (dia, semana e mês), para ajudar os gestores na tomada de decisão.

---

# 4. Requisitos Não Funcionais

**RNF01 — Desempenho**
Consultas de produtos e clientes durante o atendimento devem retornar resultados em até 2 segundos, mesmo com grande volume de registros, garantindo agilidade no balcão.

**RNF02 — Segurança**
O sistema deve autenticar usuários por credenciais únicas e registrar log de todas as operações críticas (vendas, movimentações de estoque, alterações financeiras), vinculando cada ação ao usuário responsável.

**RNF03 — Usabilidade**
A interface deve ser simples e objetiva, permitindo que atendentes realizem uma venda completa sem necessidade de treinamento extenso. Fluxos críticos devem ser concluídos com o menor número possível de telas.

**RNF04 — Confiabilidade**
O sistema deve garantir consistência entre os módulos, uma venda finalizada deve sempre atualizar o estoque e, quando a prazo, gerar o lançamento financeiro correspondente — sem possibilidade de registro parcial.

**RNF05 — Manutenibilidade**
O sistema deve ser desenvolvido com separação clara de responsabilidades entre módulos (vendas, estoque, compras, financeiro), facilitando correções e evoluções sem impacto em outros componentes.

---
