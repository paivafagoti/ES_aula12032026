### UC01 - Realizar Login
### Ator Principal
Usuário (Aluno, Recepcionista, Instrutor, Gerente)
### Objetivo
Permitir que o usuário acesse o sistema com segurança.
### Pré-condições
- Usuário deve possuir cadastro ativo.
### Pós-condições
- Sessão iniciada conforme perfil de acesso.
### Fluxo Principal
1. O usuário informa e-mail e senha.
2. O sistema valida as credenciais.
3. O sistema identifica o perfil e redireciona para a interface correspondente.
### Fluxos Alternativos
- **A1 - Senha incorreta:** O sistema exibe mensagem de erro.
### RF Relacionados
- RF01
### RNF Relacionados
- RNF02, RNF04
### RN Relacionadas
- RN06

---

### UC02 - Cadastrar Aluno
### Ator Principal
Recepcionista
### Objetivo
Registrar um novo aluno e seus dados contratuais.
### Pré-condições
- Recepcionista autenticado.
### Pós-condições
- Registro salvo na base de dados.
### Fluxo Principal
1. O recepcionista insere dados pessoais, contato, endereço e escolhe o plano.
2. O sistema valida se os campos obrigatórios estão preenchidos.
3. O sistema confirma a gravação do registro.
### RF Relacionados
- RF01, RF02
### RNF Relacionados
- RNF02
### RN Relacionadas
- RN06

---

### UC03 - Criar Novo Plano
### Ator Principal
Gerente
### Objetivo
Configurar novas modalidades de planos (ex: trimestral, funcional).
### Pré-condições
- Acesso de perfil Gerente.
### Pós-condições
- Novo plano disponível para venda na recepção.
### Fluxo Principal
1. O gerente define nome, valor e periodicidade do plano.
2. O sistema registra o plano como "Ativo".
### RF Relacionados
- RF02
### RN Relacionadas
- RN06

---

### UC04 - Registrar Pagamento na Recepção
### Ator Principal
Recepcionista
### Objetivo
Efetivar a quitação de mensalidades em dinheiro, cartão ou PIX.
### Pré-condições
- Aluno possuir pendência gerada.
### Pós-condições
- Mensalidade marcada como paga; Regularidade atualizada.
### Fluxo Principal
1. O recepcionista seleciona o aluno e a fatura.
2. Informa o método de pagamento.
3. O sistema processa o valor integral.
4. O sistema atualiza o status de acesso do aluno.
### RF Relacionados
- RF03, RF04
### RNF Relacionados
- RNF03
### RN Relacionadas
- RN04, RN07

---

### UC05 - Controlar Acesso via Catraca
### Ator Principal
Sistema de Catraca (API)
### Objetivo
Validar a entrada física do aluno na unidade.
### Pré-condições
- Aluno aproximar tag RFID na catraca.
### Pós-condições
- Acesso liberado ou bloqueado; Log de acesso gerado.
### Fluxo Principal
1. A catraca envia o ID via JSON para a API do sistema.
2. O sistema verifica a regularidade financeira.
3. Se o atraso for menor ou igual a 5 dias, o sistema envia comando de liberação.
### Fluxos Alternativos
- **A1 - Inadimplência > 5 dias:** O sistema retorna comando de bloqueio.
### RF Relacionados
- RF04, RF05
### RNF Relacionados
- RNF03, RNF06
### RN Relacionadas
- RN01

---

### UC06 - Reservar Vaga em Aula
### Ator Principal
Aluno
### Objetivo
Garantir uma vaga em aula coletiva.
### Pré-condições
- Aluno logado; Vagas disponíveis na aula.
### Pós-condições
- Reserva efetuada e notificação enviada.
### Fluxo Principal
1. O aluno escolhe a aula e o horário.
2. O sistema verifica se o limite de alunos foi atingido.
3. O sistema confirma a reserva e envia notificação.
### Fluxos Alternativos
- **A1 - Turma lotada:** O sistema impede o agendamento.
### RF Relacionados
- RF06, RF10
### RN Relacionadas
- RN02

---

### UC07 - Cancelar Agendamento de Aula
### Ator Principal
Aluno
### Objetivo
Desistir da vaga reservada em uma aula.
### Pré-condições
- Aluno possuir reserva ativa.
### Pós-condições
- Vaga liberada para outros alunos.
### Fluxo Principal
1. O aluno solicita o cancelamento da reserva.
2. O sistema valida se o horário atual é anterior a 1 hora do início da aula.
3. O sistema confirma a exclusão do agendamento.
### Fluxos Alternativos
- **A1 - Tempo limite excedido:** O sistema impede o cancelamento.
### RF Relacionados
- RF06
### RN Relacionadas
- RN03

---

### UC08 - Registrar Presença em Aula
### Ator Principal
Instrutor
### Objetivo
Listar alunos presentes para controle de ocupação.
### Pré-condições
- Aula em andamento ou finalizada.
### Pós-condições
- Lista de presença salva.
### Fluxo Principal
1. O instrutor seleciona a aula no tablet/celular.
2. O sistema apresenta a lista de alunos agendados.
3. O instrutor marca os presentes e salva.
### RF Relacionados
- RF07
### RNF Relacionados
- RNF04
### RN Relacionadas
- RN06

---

### UC09 - Realizar Avaliação Física
### Ator Principal
Instrutor
### Objetivo
Registrar métricas corporais do aluno.
### Pré-condições
- Aluno estar ativo e regular.
### Pós-condições
- Laudo disponível e notificação enviada ao aluno.
### Fluxo Principal
1. O instrutor inicia o formulário de avaliação.
2. Preenche peso, IMC e percentual de gordura.
3. O sistema salva os dados e notifica o aluno da liberação.
### Fluxos Alternativos
- **A1 - Aluno Irregular:** O sistema impede o registro da avaliação.
### RF Relacionados
- RF08, RF10
### RN Relacionadas
- RN05, RN06

---

### UC10 - Emitir Relatório de Inadimplência
### Ator Principal
Gerente
### Objetivo
Identificar alunos com débitos pendentes.
### Pré-condições
- Acesso gerencial.
### Pós-condições
- Lista de inadimplentes exibida em tela.
### Fluxo Principal
1. O gerente solicita o relatório de inadimplência.
2. O sistema filtra alunos com mensalidades vencidas.
3. O sistema exibe o tempo de atraso de cada registro.
### RF Relacionados
- RF09
### RN Relacionadas
- RN06

---

### UC11 - Notificar Vencimento de Mensalidade
### Ator Principal
Sistema (Automático)
### Objetivo
Alertar o aluno antes ou no dia do vencimento.
### Pré-condições
- Mensalidade próxima da data de expiração.
### Pós-condições
- Mensagem enviada para o dispositivo do aluno.
### Fluxo Principal
1. O sistema varre a base de dados diariamente.
2. Identifica faturas que vencem no dia.
3. Dispara notificação push/e-mail para o aluno.
### RF Relacionados
- RF10
### RNF Relacionados
- RNF01

---

### UC12 - Editar Plano Existente
### Ator Principal
Gerente
### Objetivo
Alterar valores ou descrições de planos ativos.
### Pré-condições
- Perfil Gerente autenticado.
### Pós-condições
- Plano atualizado no banco de dados.
### Fluxo Principal
1. O gerente seleciona o plano.
2. Altera o valor integral ou o nome.
3. O sistema salva a nova configuração.
### RF Relacionados
- RF02
### RN Relacionadas
- RN06

---

### UC13 - Consultar Histórico de Acessos
### Ator Principal
Gerente
### Objetivo
Auditar as entradas de alunos por período.
### Pré-condições
- Acesso gerencial.
### Pós-condições
- Relatório de log apresentado.
### Fluxo Principal
1. O gerente seleciona um período de datas.
2. O sistema lista todos os acessos registrados via API da catraca.
### RF Relacionados
- RF09
### RNF Relacionados
- RNF05

---

### UC14 - Desativar Plano
### Ator Principal
Gerente
### Objetivo
Retirar um plano da lista de vendas sem apagar o histórico.
### Pré-condições
- Plano estar atualmente ativo.
### Pós-condições
- Plano marcado como inativo.
### Fluxo Principal
1. O gerente localiza o plano.
2. Altera o status para "Desativado".
3. O sistema impede novas matrículas nesse plano.
### RF Relacionados
- RF02

---

### UC15 - Visualizar Ocupação das Aulas
### Ator Principal
Gerente
### Objetivo
Analisar quais horários e aulas estão mais cheios.
### Fluxo Principal
1. O gerente solicita relatório de ocupação.
2. O sistema exibe a porcentagem de vagas preenchidas vs total.
### RF Relacionados
- RF09

---

### UC16 - Emitir Relatório de Alunos Ativos
### Ator Principal
Gerente
### Objetivo
Contabilizar o total de clientes pagantes e regulares.
### Fluxo Principal
1. O gerente acessa o módulo de relatórios.
2. O sistema gera a contagem total de matrículas com status ativo.
### RF Relacionados
- RF09

---

### UC17 - Anexar Arquivo à Avaliação Física
### Ator Principal
Instrutor
### Objetivo
Incluir fotos ou exames externos ao registro do aluno.
### Pré-condições
- UC09 em andamento.
### Fluxo Principal
1. O instrutor seleciona a opção "Anexar Arquivo".
2. O sistema faz o upload e vincula ao prontuário.
### RF Relacionados
- RF08
### RNF Relacionados
- RNF02

---

### UC18 - Atualizar Dados de Contato
### Ator Principal
Recepcionista
### Objetivo
Manter informações do aluno em dia.
### Fluxo Principal
1. O recepcionista busca o aluno.
2. Altera telefone ou endereço.
3. O sistema valida e salva.
### RF Relacionados
- RF01

---

### UC19 - Gerar Boletos para Pagamento Online
### Ator Principal
Sistema (Automático/Aluno)
### Objetivo
Permitir o pagamento sem necessidade de ir à recepção.
### Fluxo Principal
1. O sistema gera o título de cobrança.
2. O aluno acessa o link de pagamento.
3. O sistema disponibiliza o boleto ou linha digitável.
### RF Relacionados
- RF03

---

### UC20 - Verificar Regularidade do Aluno
### Ator Principal
Sistema (Automático)
### Objetivo
Garantir que o status do aluno reflita seu estado financeiro real.
### Pós-condições
- Status atualizado para Ativo ou Inadimplente.
### Fluxo Principal
1. O sistema verifica pagamentos vinculados à matrícula.
2. Compara a data de vencimento com a data atual.
3. Se houver débito não pago, marca o aluno como irregular.
### RF Relacionados
- RF04
### RN Relacionadas
- RN07
