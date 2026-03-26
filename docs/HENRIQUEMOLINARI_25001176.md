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

**Justificativa:**

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

 # 🛡 4. Requisitos Não Funcionais

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
# 5. Casos de Uso

<img width="484" height="1009" alt="image" src="https://github.com/user-attachments/assets/a46b0319-e92a-4bf9-8a0f-6b74ff4f2b47" />
# 6. Documentação dos Casos de Uso

---

## UC01 — Realizar Venda

**Ator(es):** Atendente, Administrador

**Descrição:** Registra a venda de produtos a um cliente, verificando estoque, calculando valores e emitindo comprovante ao final.

**Pré-condições:**
- Usuário autenticado com perfil Atendente ou superior
- Produtos cadastrados no sistema com estoque disponível

**Pós-condições:**
- Venda registrada no sistema
- Estoque da unidade atualizado
- Comprovante emitido ao cliente

### Fluxo Principal
1. Atendente inicia uma nova venda
2. Sistema solicita identificação do cliente *(inclui UC02)*
3. Atendente pesquisa e adiciona produtos pelo nome ou código de barras
4. Sistema verifica disponibilidade em estoque para cada item *(inclui UC03)*
5. Atendente informa as quantidades desejadas
6. Sistema calcula e exibe o valor total
7. Atendente seleciona a forma de pagamento (à vista)
8. Sistema finaliza a venda, atualiza o estoque e emite o comprovante

### Fluxos Alternativos / Exceções
- FA01 — Estoque insuficiente: o sistema bloqueia o item, informa o saldo disponível e aguarda nova quantidade ou remoção do produto
- FA02 — Produto não encontrado: o sistema exibe mensagem de erro e permite nova busca

### Relacionamentos
- **Include:** UC02 — Identificar ou Cadastrar Cliente; UC03 — Consultar e Verificar Estoque
- **Extend:** UC04 — Registrar Venda a Prazo (quando forma de pagamento for a prazo); UC05 — Validar Receita Médica (quando produto for controlado)

### Diagrama de Atividades
<img width="472" height="1290" alt="image" src="https://github.com/user-attachments/assets/60c1a180-9450-42df-be34-48101b008be2" />

---

## UC02 — Identificar ou Cadastrar Cliente

**Ator(es):** Atendente

**Descrição:** Localiza o cliente no sistema pelo CPF ou nome. Caso não esteja cadastrado, permite o registro rápido durante o atendimento.

**Pré-condições:**
- Venda em andamento (UC01 em execução)

**Pós-condições:**
- Cliente identificado e vinculado à venda
- Novo cadastro criado, se necessário

### Fluxo Principal
1. Sistema solicita CPF ou nome do cliente
2. Atendente informa os dados
3. Sistema localiza o cadastro existente
4. Cliente é vinculado à venda em andamento

### Fluxos Alternativos / Exceções
- FA01 — Cliente não encontrado: o sistema oferece a opção de cadastrar novo cliente com nome, CPF e contato
- FA02 — Atendimento sem identificação: venda pode ser registrada como "consumidor final", sem vínculo a cadastro

### Relacionamentos
- **Include:** Nenhum
- **Extend:** Nenhum

### Diagrama de Atividades
<img width="605" height="501" alt="image" src="https://github.com/user-attachments/assets/6918355a-1c7c-4dfd-9192-ea782ab85665" />

---

## UC03 — Consultar e Verificar Estoque

**Ator(es):** Atendente, Gerente

**Descrição:** Verifica a disponibilidade de um produto no estoque da unidade antes de confirmar sua inclusão em uma venda.

**Pré-condições:**
- Produto selecionado na venda
- Estoque da unidade atualizado no sistema

**Pós-condições:**
- Quantidade disponível confirmada ou insuficiência informada
- Alerta emitido se saldo estiver abaixo do mínimo

### Fluxo Principal
1. Sistema recebe o código do produto e a quantidade solicitada
2. Sistema consulta o saldo atual em estoque da unidade
3. Sistema compara a quantidade solicitada com o saldo disponível
4. Disponibilidade confirmada e retornada ao fluxo de venda

### Fluxos Alternativos / Exceções
- FA01 — Estoque insuficiente: sistema retorna saldo disponível e bloqueia a quantidade solicitada
- FA02 — Produto sem registro de estoque: sistema informa que o produto não possui saldo cadastrado na unidade

### Relacionamentos
- **Include:** Nenhum
- **Extend:** UC10 — Emitir Alerta de Estoque Mínimo (quando saldo atingir nível mínimo)

### Diagrama de Atividades

<img width="466" height="691" alt="image" src="https://github.com/user-attachments/assets/6c69a210-bc80-4d86-82e9-2548c4300b12" />

---

## UC04 — Registrar Venda a Prazo

**Ator(es):** Atendente

**Descrição:** Estende uma venda comum quando o cliente opta por pagamento a prazo, gerando automaticamente o lançamento em contas a receber.

**Pré-condições:**
- Venda em andamento com cliente identificado e cadastrado
- Forma de pagamento selecionada como "a prazo"

**Pós-condições:**
- Venda finalizada
- Lançamento criado em contas a receber com status "Aberta"

### Fluxo Principal
1. Atendente seleciona forma de pagamento "a prazo"
2. Sistema solicita a data de vencimento
3. Atendente informa o prazo acordado
4. Sistema cria lançamento em contas a receber com valor, vencimento e status "Aberta"
5. Venda é finalizada normalmente

### Fluxos Alternativos / Exceções
- FA01 — Cliente sem cadastro completo: sistema impede venda a prazo e solicita complemento dos dados do cliente
- FA02 — Data de vencimento inválida: sistema rejeita a data e solicita nova informação

### Relacionamentos
- **Include:** Nenhum
- **Extend:** Estende UC01 — Realizar Venda

### Diagrama de Atividades
<img width="274" height="900" alt="image" src="https://github.com/user-attachments/assets/8930cc93-4895-4e26-a6c3-7c594d7abf8f" />

---

## UC05 — Validar Receita Médica

**Ator(es):** Farmacêutico

**Descrição:** Verifica e registra a receita médica apresentada pelo cliente antes de autorizar a venda de medicamento controlado.

**Pré-condições:**
- Venda em andamento contendo produto de controle especial
- Farmacêutico autenticado no sistema

**Pós-condições:**
- Receita registrada e venda autorizada, ou venda bloqueada por ausência/irregularidade da receita

### Fluxo Principal
1. Sistema identifica produto controlado na venda e aciona validação
2. Farmacêutico analisa a receita apresentada pelo cliente
3. Farmacêutico registra os dados da receita no sistema (número, médico, data)
4. Sistema autoriza a continuidade da venda

### Fluxos Alternativos / Exceções
- FA01 — Receita ausente: farmacêutico rejeita a autorização e sistema bloqueia a venda do item controlado
- FA02 — Receita vencida ou irregular: sistema registra a ocorrência e bloqueia o item

### Relacionamentos
- **Include:** Nenhum
- **Extend:** Estende UC01 — Realizar Venda

### Diagrama de Atividades
<img width="257" height="804" alt="image" src="https://github.com/user-attachments/assets/f9a3f689-3c47-42e9-adaa-d2f3491bf8fe" />

---

## UC06 — Registrar Compra de Fornecedor

**Ator(es):** Gerente, Administrador

**Descrição:** Registra a entrada de produtos adquiridos de um fornecedor, atualizando o estoque da unidade e gerando lançamento financeiro.

**Pré-condições:**
- Usuário autenticado com perfil Gerente ou Administrador
- Fornecedor e produtos cadastrados no sistema

**Pós-condições:**
- Compra registrada no sistema
- Estoque da unidade atualizado
- Lançamento criado em contas a pagar

### Fluxo Principal
1. Gerente acessa o módulo de compras e inicia novo registro
2. Seleciona o fornecedor
3. Informa os produtos adquiridos, quantidades e valores
4. Informa a data da compra e o vencimento do pagamento
5. Sistema atualiza o estoque da unidade *(inclui UC07)*
6. Sistema gera lançamento em contas a pagar *(inclui UC08)*
7. Compra registrada com sucesso

### Fluxos Alternativos / Exceções
- FA01 — Produto não cadastrado: sistema permite cadastro rápido do produto antes de continuar
- FA02 — Fornecedor não encontrado: sistema solicita cadastro do fornecedor

### Relacionamentos
- **Include:** UC07 — Atualizar Estoque; UC08 — Lançar Conta a Pagar
- **Extend:** Nenhum

### Diagrama de Atividades
<img width="390" height="764" alt="image" src="https://github.com/user-attachments/assets/56b5aae2-074d-4067-be0b-cbffe26d0f9f" />

---

## UC07 — Atualizar Estoque

**Ator(es):** Sistema (automático)

**Descrição:** Atualiza o saldo em estoque de um produto em uma unidade após qualquer movimentação registrada (compra, venda, devolução ou perda).

**Pré-condições:**
- Movimentação registrada por outro caso de uso (venda ou compra)
- Produto e unidade identificados

**Pós-condições:**
- Saldo do produto na unidade atualizado corretamente

### Fluxo Principal
1. Sistema recebe os dados da movimentação (produto, quantidade, tipo, unidade)
2. Sistema localiza o registro de estoque do produto na unidade
3. Aplica a operação correspondente (entrada ou saída)
4. Persiste o novo saldo no sistema

### Fluxos Alternativos / Exceções
- FA01 — Registro de estoque inexistente para o produto: sistema cria o registro com saldo inicial igual à quantidade movimentada (apenas para entradas)
- FA02 — Falha ao persistir: sistema registra erro e reverte a operação origem para garantir consistência

### Relacionamentos
- **Include:** É incluído por UC01 e UC06
- **Extend:** Nenhum

### Diagrama de Atividades

<img width="577" height="591" alt="image" src="https://github.com/user-attachments/assets/320d3cd7-4ec9-4d5f-8abb-89ec7ff85050" />

---

## UC08 — Lançar Conta a Pagar

**Ator(es):** Sistema (automático), Financeiro

**Descrição:** Cria um lançamento financeiro em contas a pagar a partir de uma compra registrada, com valor, vencimento e status inicial.

**Pré-condições:**
- Compra registrada com valor total e data de vencimento definidos

**Pós-condições:**
- Lançamento criado em contas a pagar com status "Aberta"

### Fluxo Principal
1. Sistema recebe os dados da compra (valor, fornecedor, vencimento)
2. Cria o lançamento com descrição, valor, data de vencimento e status "Aberta"
3. Lançamento disponível para consulta e gestão pelo setor Financeiro

### Fluxos Alternativos / Exceções
- FA01 — Data de vencimento não informada: sistema aplica a data da compra como vencimento e emite aviso
- FA02 — Falha na criação: sistema registra erro e notifica o operador para lançamento manual

### Relacionamentos
- **Include:** É incluído por UC06
- **Extend:** Nenhum

### Diagrama de Atividades

<img width="461" height="744" alt="image" src="https://github.com/user-attachments/assets/4b9c15f1-9b9c-49c8-9754-c4d7f64480f4" />

---

## UC09 — Gerenciar Contas a Receber

**Ator(es):** Financeiro, Administrador, Atendente

**Descrição:** Permite ao setor financeiro consultar, filtrar e atualizar os lançamentos de contas a receber, registrando recebimentos e acompanhando vencimentos.

**Pré-condições:**
- Usuário autenticado com perfil Financeiro, Administrador ou Atendente
- Lançamentos existentes no sistema

**Pós-condições:**
- Status dos lançamentos atualizado conforme as ações realizadas

### Fluxo Principal
1. Usuário acessa o módulo de contas a receber
2. Sistema exibe lista de lançamentos com filtros por status e período
3. Usuário seleciona um lançamento em aberto
4. Registra o recebimento informando a data e o valor recebido
5. Sistema atualiza o status para "Recebida"

### Fluxos Alternativos / Exceções
- FA01 — Lançamento vencido sem recebimento: sistema exibe status "Atrasada" e destaca o registro
- FA02 — Valor recebido diferente do original: sistema registra o valor real e mantém o saldo pendente em aberto

### Relacionamentos
- **Include:** Nenhum
- **Extend:** Nenhum

### Diagrama de Atividades
<img width="434" height="911" alt="image" src="https://github.com/user-attachments/assets/36765e02-70b6-4632-a3ea-dcc7b9e174d1" />

---

## UC10 — Emitir Alerta de Estoque Mínimo

**Ator(es):** Sistema (automático), Gerente

**Descrição:** Notifica o gerente da unidade quando o saldo de um produto atinge ou fica abaixo do nível mínimo configurado, sem bloquear as demais operações.

**Pré-condições:**
- Produto com nível mínimo de estoque configurado
- Saldo do produto igual ou inferior ao mínimo após movimentação

**Pós-condições:**
- Alerta registrado e exibido ao gerente da unidade

### Fluxo Principal
1. Sistema identifica que o saldo do produto atingiu o nível mínimo após uma movimentação
2. Sistema gera o alerta com produto, unidade e saldo atual
3. Alerta é exibido na interface do gerente da unidade
4. Gerente visualiza e decide sobre a necessidade de reposição

### Fluxos Alternativos / Exceções
- FA01 — Nível mínimo não configurado para o produto: sistema não emite alerta e registra ausência de parâmetro
- FA02 — Gerente não está ativo no sistema: alerta é mantido pendente e exibido no próximo acesso

### Relacionamentos
- **Include:** Nenhum
- **Extend:** Estende UC03 — Consultar e Verificar Estoque

### Diagrama de Atividades

<img width="494" height="710" alt="image" src="https://github.com/user-attachments/assets/b1e76c28-24f2-4e14-8144-3e0330397b71" />

---

## UC11 — Gerar Relatório de Indicadores

**Ator(es):** Gerente, Financeiro, Administrador

**Descrição:** Permite que gestores consultem relatórios simples com indicadores operacionais da unidade, como produtos mais vendidos, saldo de estoque e vendas por período.

**Pré-condições:**
- Usuário autenticado com perfil Gerente, Financeiro ou Administrador
- Dados de vendas e estoque registrados no sistema

**Pós-condições:**
- Relatório gerado e exibido ao usuário conforme os filtros aplicados

### Fluxo Principal
1. Usuário acessa o módulo de relatórios
2. Seleciona o tipo de relatório desejado (produtos mais vendidos, estoque ou vendas por período)
3. Informa os filtros necessários (período, unidade)
4. Sistema processa e exibe o relatório na tela

### Fluxos Alternativos / Exceções
- FA01 — Sem dados no período informado: sistema exibe mensagem informando ausência de registros para os filtros aplicados
- FA02 — Período inválido (data final anterior à inicial): sistema rejeita o filtro e solicita correção

### Relacionamentos
- **Include:** Nenhum
- **Extend:** Nenhum

### Diagrama de Atividades
<img width="536" height="757" alt="image" src="https://github.com/user-attachments/assets/b8f5b93f-2d2f-4c39-91fe-5f3c19cdca03" />

