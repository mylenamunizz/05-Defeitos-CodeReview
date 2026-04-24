# 📦 Relatório Final

> **Atividade:** Bug Report Profissional + Code Review Guiado
> **Curso:** Qualidade de Software
> **Professor:** Prof. Claudio Nunes

---

## 👥 Identificação da dupla

| Nome completo | RA | GitHub |
|---|---|---|
| Ana Karolina Moura | 229033 | @akarolmoura |
| Mylena Muniz Jacob | 227488 | @mylenamunizz |

**Ambiente de testes:** Chrome no Windows 11, Github Pages do Fork. 
---

## 📋 Sumário

- [Parte A — Bug Reports](#parte-a--bug-reports)
- [Parte B — Code Review](#parte-b--code-review)
- [Reflexão final](#-reflexão-final)
- [Declarações](#-declarações)

---

## Parte A — Bug Reports

> **Substitua este bloco de citação pelo conteúdo copiado integralmente do seu arquivo `parte-a-bug-report/template-bug-report.md`.**
🐛 Bug Reports — Parte A
Preencha uma seção completa para cada defeito encontrado. O mínimo exigido é 3 bug reports. Apague este bloco antes de entregar.

Dupla: Ana Karolina Moura. 229033. + Mylena Muniz Jacob. 227488. Data da exploração: 23/04/2026. Navegador usado: Chrome. Sistema operacional: Windows 11.

BUG-001
Título: O sistema permite que tarefas "vazias" sejam entregues, sem título, data e prioridade definidas.

Severidade: Crítica Justificativa da severidade: Os campos deveriam ser de preenchimento obrigatório para o site cumprir a sua principal função.

Prioridade: P1 Justificativa da prioridade: Impede o funcionamento correto da funcionalidade principal do sistema, afetando diretamente a usabilidade.

Ambiente:

Navegador: Chrome.
Sistema Operacional: Windows 11.
Versão da aplicação: TarefaQS v1.0.0
Passos para reprodução:

Acessar a aplicação TarefaQS
Iniciar a criação de uma nova tarefa
Deixar os campos de título, data e prioridade em branco
Confirmar/salvar a tarefa
Resultado esperado: O sistema deveria exibir mensagens de validação nos campos obrigatórios (título, data e prioridade) e impedir o salvamento da tarefa enquanto esses campos não forem preenchidos.

Resultado obtido: A tarefa é salva com sucesso mesmo com todos os campos obrigatórios vazios, sem qualquer mensagem de erro ou bloqueio por parte do sistema.

Evidência:image

Sugestão de causa raiz (opcional): Ausência de validação dos campos obrigatórios no frontend antes do envio do formulário, e possivelmente também no backend, permitindo que registros incompletos sejam persistidos.

BUG-002
Título: O sistema deveria exibir uma mensagem de validação impedindo o uso de emojis no título, aceitando apenas caracteres de texto padrão.

Severidade: P4 Justificativa da severidade: Emojis no título não impedem o funcionamento do sistema, mas podem causar problemas de exibição, encoding ou integração com outros sistemas.

Prioridade: P3 Justificativa da prioridade: Não é urgente, mas deve ser corrigido para garantir a integridade dos dados e consistência da interface.

Ambiente:

Navegador:
Sistema Operacional:
Versão da aplicação: TarefaQS v1.0.0
Passos para reprodução:

Acessar a aplicação TarefaQS
Iniciar a criação de uma nova tarefa
Inserir um emoji no campo de título
Preencher os demais campos e salvar a tarefa
Resultado esperado: O sistema deveria exibir uma mensagem de validação informando que o campo de título não aceita emojis, bloqueando o salvamento até que o título contenha apenas caracteres de texto padrão.

Resultado obtido: A tarefa é salva normalmente com o emoji no título, sem qualquer mensagem de aviso ou bloqueio por parte do sistema.

Evidência:image

Sugestão de causa raiz (opcional): Ausência de validação/sanitização do campo de título para restringir caracteres ao conjunto de texto padrão (sem Unicode estendido/emojis).

BUG-003
Título: O sistema aceita valores de prioridade fora do intervalo permitido (1 a 5).

Severidade: Alta Justificativa da severidade: O campo de prioridade é essencial para a organização das tarefas. Aceitar valores fora do intervalo compromete a lógica de priorização e a integridade dos dados.

Prioridade: P2 Justificativa da prioridade: Afeta diretamente uma funcionalidade central do sistema, mas não impede completamente o uso da aplicação.

Ambiente:

Navegador: Chrome.
Sistema Operacional:Windows 11.
Versão da aplicação: TarefaQS v1.0.0
Passos para reprodução:

Acessar a aplicação TarefaQS v1.0.0
Iniciar a criação de uma nova tarefa
Preencher o campo de prioridade com um valor fora do intervalo permitido (ex: 70)
Preencher os demais campos e salvar a tarefa
Resultado esperado: O sistema deveria exibir uma mensagem de validação informando que o campo de prioridade aceita apenas valores entre 1 e 5, bloqueando o salvamento até que um valor válido seja inserido.

Resultado obtido: A tarefa é salva normalmente com o valor 70 no campo de prioridade, sem qualquer mensagem de aviso ou bloqueio por parte do sistema.

Evidência:image

Sugestão de causa raiz (opcional): Ausência de validação do campo de prioridade para restringir a entrada ao intervalo permitido (1 a 5), permitindo que qualquer valor numérico seja aceito e persistido sem restrições.

✅ Critérios de qualidade do bug report
(Use para conferir antes de entregar)

 Título descritivo — outra pessoa entende o problema só pelo título?
 Passos são numerados e reproduzíveis por terceiros?
 Há pelo menos uma evidência (screenshot, GIF ou log)?
 Severidade tem justificativa explícita?
 Prioridade tem justificativa explícita?
 Ambiente inclui navegador + SO?
 "Esperado vs. Obtido" deixa o gap claro?
✅ Checklist de qualidade dos reports
Antes de submeter, confirme em cada report:

 Título é específico e acionável (não "Não funciona").
 Passos estão numerados e são reproduzíveis por terceiros.
 Há pelo menos uma evidência por report (imagem, GIF ou log).
 Severidade tem justificativa explícita.
 Prioridade tem justificativa explícita.
 Ambiente inclui navegador + SO.
 "Esperado × Obtido" deixa a diferença clara.
 Os 3 defeitos reportados cobrem categorias diferentes (funcional, UX, validação, persistência, etc.)

---

## Parte B — Code Review

> **Substitua este bloco de citação pelo conteúdo copiado integralmente do seu arquivo `parte-b-code-review/formulario-code-review.md`.**
🔎 Formulário — Parte B
Preencha uma seção por finding. O mínimo esperado é 6 findings.

Dupla: Ana Karolina Moura. 229033. + Mylena Muniz Jacob. 227488. Data da revisão: 23/04/2026.

Finding #1
📍 Linha(s): 12/13. 🏷 Rótulo: blocker. 📂 Dimensão: Segurança. ⚠️ Severidade: Crítica.

🐛 Problema: A função buscarUsuarioPorNome concatena diretamente o parâmetro nome na query SQL, permitindo SQL Injection. Um atacante pode passar ' OR '1'='1 e retornar todos os registros do banco.

💡 Sugestão de correção: async function buscarUsuarioPorNome(nome) { return db.executarQuery('SELECT * FROM usuarios WHERE nome = ?', [nome]); }

Finding #2
📍 Linha(s): 20. 🏷 Rótulo: blocker. 📂 Dimensão: Segurança. ⚠️ Severidade: Crítica.

🐛 Problema: O campo tipo é persistido no banco sem nenhuma validação, mesmo existindo a constante TIPOS_VALIDOS declarada no arquivo. Valores arbitrários como "admin" ou "superuser" poderiam ser inseridos sem restrição.

💡 Sugestão de correção: if (!TIPOS_VALIDOS.includes(dados.tipo)) { throw new Error(Tipo inválido. Valores aceitos: ${TIPOS_VALIDOS.join(', ')}); }

Finding #3
📍 Linha(s): 26. 🏷 Rótulo: major. 📂 Dimensão: Segurança. ⚠️ Severidade: Alta.

🐛 Problema: O objeto usuario retornado por cadastrarUsuario inclui o campo senha (mesmo que hasheado). Expor o hash em respostas é uma má prática de segurança, pois facilita ataques de força bruta offline caso o dado seja interceptado ou logado.

💡 Sugestão de correção: const { senha, ...usuarioSemSenha } = usuario; return usuarioSemSenha;

Finding #4
📍 Linha(s): 32-35. 🏷 Rótulo: blocker. 📂 Dimensão: Erros. ⚠️ Severidade: Alta.

🐛 Problema: A função atualizarEmail não trata o caso em que buscarPorId retorna null ou undefined. Se o id não existir no banco, a linha u.email = novoEmail lançará TypeError: Cannot set properties of null, quebrando a aplicação. Além disso, não há validação de formato do novoEmail.

💡 Sugestão de correção: async function atualizarEmail(id, novoEmail) { const u = await db.buscarPorId('usuarios', id); if (!u) throw new Error('Usuário não encontrado'); if (!novoEmail || !novoEmail.includes('@')) throw new Error('Email inválido'); u.email = novoEmail; await db.atualizar('usuarios', id, u); logger.info('Email atualizado: ' + novoEmail); return u; }

Finding #5
📍 Linha(s): 43 🏷 Rótulo: nit. 📂 Dimensão: Legibilidade. ⚠️ Severidade: Baixa.

🐛 Problema: A variável hoje é declarada no início de calcularLimiteEmprestimo, mas só é utilizada no bloco final de verificação de bloqueadoAte. Isso cria a falsa impressão de que a data atual influencia toda a lógica da função, prejudicando a legibilidade

💡 Sugestão de correção: // Mover a declaração para próximo do único bloco que a utiliza if (usuario.bloqueadoAte) { const hoje = new Date(); if (new Date(usuario.bloqueadoAte) > hoje) return 0; }

Finding #6
📍 Linha(s): 43–100 vs. 103–105 🏷 Rótulo: Major. 📂 Dimensão: Complexidade. ⚠️ Severidade: Média.

🐛 Problema: A verificação de bloqueadoAte ocorre ao final de calcularLimiteEmprestimo, após toda a lógica de cálculo ser executada desnecessariamente. Isso é inconsistente com calcularLimiteComSuspensao, que verifica a suspensão logo no início da função, e representa desperdício de processamento e risco de comportamento inesperado.

💡 Sugestão de correção: function calcularLimiteEmprestimo(usuario) { // Verificação antecipada, igual ao padrão de calcularLimiteComSuspensao if (usuario.bloqueadoAte && new Date(usuario.bloqueadoAte) > new Date()) { return 0; }

let limite = 5; // ... restante da lógica }

✅ Checklist final
 Há pelo menos 6 findings preenchidas
 Cada finding cita linha, dimensão, rótulo e severidade
 As sugestões são concretas e acionáveis
 Pelo menos uma finding cobre segurança
 Pelo menos uma finding cobre complexidade

 
### Resumo

| # | Linha | Dimensão     | Rótulo      | Severidade |
|---|-------|--------------|------------ |------------|
| 1 | 12-13 | Segurança    | blocker     |  Crítica   |
| 2 | 20    | Segurança    | blocker     |  Crítica   |
| 3 | 26    | Segurança    | major       |  Alta      |
| 4 | 32-35 | Erros        | blocker     |  Alta      |
| 5 | 43    | Legibilidade | nlt         |  Baixa     |
| 6 |43-105 | Complexidade | major       |  Média     |

### Findings detalhadas

Finding #1
📍 Linha(s): 12/13. 🏷 Rótulo: blocker. 📂 Dimensão: Segurança. ⚠️ Severidade: Crítica.

🐛 Problema: A função buscarUsuarioPorNome concatena diretamente o parâmetro nome na query SQL, permitindo SQL Injection. Um atacante pode passar ' OR '1'='1 e retornar todos os registros do banco.

💡 Sugestão de correção: async function buscarUsuarioPorNome(nome) { return db.executarQuery('SELECT * FROM usuarios WHERE nome = ?', [nome]); }

Finding #2
📍 Linha(s): 20. 🏷 Rótulo: blocker. 📂 Dimensão: Segurança. ⚠️ Severidade: Crítica.

🐛 Problema: O campo tipo é persistido no banco sem nenhuma validação, mesmo existindo a constante TIPOS_VALIDOS declarada no arquivo. Valores arbitrários como "admin" ou "superuser" poderiam ser inseridos sem restrição.

💡 Sugestão de correção: if (!TIPOS_VALIDOS.includes(dados.tipo)) { throw new Error(Tipo inválido. Valores aceitos: ${TIPOS_VALIDOS.join(', ')}); }

Finding #3
📍 Linha(s): 26. 🏷 Rótulo: major. 📂 Dimensão: Segurança. ⚠️ Severidade: Alta.

🐛 Problema: O objeto usuario retornado por cadastrarUsuario inclui o campo senha (mesmo que hasheado). Expor o hash em respostas é uma má prática de segurança, pois facilita ataques de força bruta offline caso o dado seja interceptado ou logado.

💡 Sugestão de correção: const { senha, ...usuarioSemSenha } = usuario; return usuarioSemSenha;

Finding #4
📍 Linha(s): 32-35. 🏷 Rótulo: blocker. 📂 Dimensão: Erros. ⚠️ Severidade: Alta.

🐛 Problema: A função atualizarEmail não trata o caso em que buscarPorId retorna null ou undefined. Se o id não existir no banco, a linha u.email = novoEmail lançará TypeError: Cannot set properties of null, quebrando a aplicação. Além disso, não há validação de formato do novoEmail.

💡 Sugestão de correção: async function atualizarEmail(id, novoEmail) { const u = await db.buscarPorId('usuarios', id); if (!u) throw new Error('Usuário não encontrado'); if (!novoEmail || !novoEmail.includes('@')) throw new Error('Email inválido'); u.email = novoEmail; await db.atualizar('usuarios', id, u); logger.info('Email atualizado: ' + novoEmail); return u; }

Finding #5
📍 Linha(s): 43 🏷 Rótulo: nit. 📂 Dimensão: Legibilidade. ⚠️ Severidade: Baixa.

🐛 Problema: A variável hoje é declarada no início de calcularLimiteEmprestimo, mas só é utilizada no bloco final de verificação de bloqueadoAte. Isso cria a falsa impressão de que a data atual influencia toda a lógica da função, prejudicando a legibilidade

💡 Sugestão de correção: // Mover a declaração para próximo do único bloco que a utiliza if (usuario.bloqueadoAte) { const hoje = new Date(); if (new Date(usuario.bloqueadoAte) > hoje) return 0; }

Finding #6
📍 Linha(s): 43–100 vs. 103–105 🏷 Rótulo: Major. 📂 Dimensão: Complexidade. ⚠️ Severidade: Média.

🐛 Problema: A verificação de bloqueadoAte ocorre ao final de calcularLimiteEmprestimo, após toda a lógica de cálculo ser executada desnecessariamente. Isso é inconsistente com calcularLimiteComSuspensao, que verifica a suspensão logo no início da função, e representa desperdício de processamento e risco de comportamento inesperado.

💡 Sugestão de correção: function calcularLimiteEmprestimo(usuario) { // Verificação antecipada, igual ao padrão de calcularLimiteComSuspensao if (usuario.bloqueadoAte && new Date(usuario.bloqueadoAte) > new Date()) { return 0; }

let limite = 5; // ... restante da lógica }
---

## 💭 Reflexão final

> Responda em 1-2 parágrafos. Esta reflexão **é obrigatória**.

**Qual dimensão do checklist foi mais difícil aplicar? Por quê?**

A dimensão de Complexidade foi a mais desafiadora de aplicar. Diferente de Segurança, onde os problemas têm sinais claros e referências consolidadas como as da OWASP, a complexidade exige comparar trechos distintos do código entre si e entender a intenção original do autor. No caso das funções calcularLimiteEmprestimo e calcularLimiteComSuspensao, foi necessário ler as duas implementações em paralelo para perceber a inconsistência na ordem das verificações — algo que não seria óbvio analisando apenas uma delas isoladamente.

**O que vocês fariam diferente se revisassem o código novamente?**

Começaríamos mapeando as funções exportadas e suas responsabilidades antes de entrar linha a linha, o que ajudaria a identificar mais rapidamente inconsistências entre funções que fazem coisas semelhantes, como as duas funções de cálculo de limite. Também adicionaríamos desde o início uma coluna de "intenção esperada" para cada trecho analisado, facilitando distinguir se o problema é de implementação incorreta ou de design da função — o que torna as sugestões de correção mais precisas e úteis para o desenvolvedor.
---

## 📣 Declarações


### Uso de IA como parceiro de trabalho

- [ ] Não usamos IA nesta atividade.
- [x] Usamos IA para esclarecer conceitos teóricos.
- [x] Usamos IA para revisar a redação dos bug reports.
- [x] Usamos IA para discutir se um achado era ou não um defeito.
- [ ] Uso específico: [descreva]

### Declaração de autoria

Declaramos que este relatório é de autoria da dupla, que exploramos
pessoalmente a aplicação da Parte A e lemos o código da Parte B. As
findings aqui registradas representam nosso próprio julgamento
técnico.
