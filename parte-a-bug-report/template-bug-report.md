# 🐛 Bug Reports — Parte A

> Preencha uma seção completa para cada defeito encontrado. O mínimo
> exigido é **3 bug reports**. Apague este bloco antes de entregar.

**Dupla:** Ana Karolina Moura. 229033. + Mylena Muniz Jacob. 227488.
**Data da exploração:** 23/04/2026.
**Navegador usado:** Chrome.
**Sistema operacional:** Windows 11.

---

## BUG-001

**Título:** O sistema permite que tarefas "vazias" sejam entregues, sem título, data e prioridade definidas.

**Severidade:** Crítica 
**Justificativa da severidade:** Os campos deveriam ser de preenchimento obrigatório para o site cumprir a sua principal função.

**Prioridade:** P1
**Justificativa da prioridade:** Impede o funcionamento correto da funcionalidade principal do sistema, afetando diretamente a usabilidade.

**Ambiente:**
- Navegador: Chrome.
- Sistema Operacional: Windows 11.
- Versão da aplicação: TarefaQS v1.0.0

**Passos para reprodução:**
1. Acessar a aplicação TarefaQS 
2. Iniciar a criação de uma nova tarefa
3. Deixar os campos de título, data e prioridade em branco
4. Confirmar/salvar a tarefa

**Resultado esperado:**
O sistema deveria exibir mensagens de validação nos campos obrigatórios (título, data e prioridade) e impedir o salvamento da tarefa enquanto esses campos não forem preenchidos.

**Resultado obtido:**
A tarefa é salva com sucesso mesmo com todos os campos obrigatórios vazios, sem qualquer mensagem de erro ou bloqueio por parte do sistema.

**Evidência:**
<img width="1587" height="929" alt="image" src="https://github.com/user-attachments/assets/2ae8df85-82f0-4a0e-9380-dce6d3a13a70" />

**Sugestão de causa raiz (opcional):**
Ausência de validação dos campos obrigatórios no frontend antes do envio do formulário, e possivelmente também no backend, permitindo que registros incompletos sejam persistidos.

---

## BUG-002

**Título:** O sistema deveria exibir uma mensagem de validação impedindo o uso de emojis no título, aceitando apenas caracteres de texto padrão.

**Severidade:** P4
**Justificativa da severidade:** Emojis no título não impedem o funcionamento do sistema, mas podem causar problemas de exibição, encoding ou integração com outros sistemas.

**Prioridade:** P3
**Justificativa da prioridade:** Não é urgente, mas deve ser corrigido para garantir a integridade dos dados e consistência da interface.

**Ambiente:**
- Navegador:
- Sistema Operacional:
- Versão da aplicação: TarefaQS v1.0.0

**Passos para reprodução:**
1. Acessar a aplicação TarefaQS 
2. Iniciar a criação de uma nova tarefa
3. Inserir um emoji no campo de título
4. Preencher os demais campos e salvar a tarefa

**Resultado esperado:** O sistema deveria exibir uma mensagem de validação informando que o campo de título não aceita emojis, bloqueando o salvamento até que o título contenha apenas caracteres de texto padrão.

**Resultado obtido:** A tarefa é salva normalmente com o emoji no título, sem qualquer mensagem de aviso ou bloqueio por parte do sistema.

**Evidência:**
<img width="1677" height="895" alt="image" src="https://github.com/user-attachments/assets/75354b8c-1b50-4448-83f0-75694ad4715a" />

**Sugestão de causa raiz (opcional):** Ausência de validação/sanitização do campo de título para restringir caracteres ao conjunto de texto padrão (sem Unicode estendido/emojis).

---

## BUG-003

**Título:** O sistema aceita valores de prioridade fora do intervalo permitido (1 a 5).

**Severidade:** Alta
**Justificativa da severidade:** O campo de prioridade é essencial para a organização das tarefas. Aceitar valores fora do intervalo compromete a lógica de priorização e a integridade dos dados.

**Prioridade:** P2
**Justificativa da prioridade:** Afeta diretamente uma funcionalidade central do sistema, mas não impede completamente o uso da aplicação.

**Ambiente:**
- Navegador: Chrome.
- Sistema Operacional:Windows 11.
- Versão da aplicação: TarefaQS v1.0.0

**Passos para reprodução:**
1. Acessar a aplicação TarefaQS v1.0.0
2. Iniciar a criação de uma nova tarefa
3. Preencher o campo de prioridade com um valor fora do intervalo permitido (ex: 70)
4. Preencher os demais campos e salvar a tarefa

**Resultado esperado:** O sistema deveria exibir uma mensagem de validação informando que o campo de prioridade aceita apenas valores entre 1 e 5, bloqueando o salvamento até que um valor válido seja inserido.

**Resultado obtido:** A tarefa é salva normalmente com o valor 70 no campo de prioridade, sem qualquer mensagem de aviso ou bloqueio por parte do sistema.

**Evidência:** 
<img width="1520" height="839" alt="image" src="https://github.com/user-attachments/assets/4aecf184-d86d-4ac1-96d5-936f8b2fd0ca" />

**Sugestão de causa raiz (opcional):** Ausência de validação do campo de prioridade para restringir a entrada ao intervalo permitido (1 a 5), permitindo que qualquer valor numérico seja aceito e persistido sem restrições.

---

<!-- Para reports adicionais, copie o bloco acima trocando o número. -->

---

## ✅ Critérios de qualidade do bug report
*(Use para conferir antes de entregar)*

- [x] Título descritivo — outra pessoa entende o problema só pelo título?
- [x] Passos são **numerados** e **reproduzíveis** por terceiros?
- [x] Há **pelo menos uma evidência** (screenshot, GIF ou log)?
- [x] Severidade tem **justificativa explícita**?
- [x] Prioridade tem **justificativa explícita**?
- [x] Ambiente inclui **navegador + SO**?
- [x] "Esperado vs. Obtido" deixa o gap claro?

## ✅ Checklist de qualidade dos reports

Antes de submeter, confirme em cada report:

- [x] Título é específico e acionável (não `"Não funciona"`).
- [x] Passos estão **numerados** e são reproduzíveis por terceiros.
- [x] Há **pelo menos uma evidência** por report (imagem, GIF ou log).
- [x] Severidade tem **justificativa explícita**.
- [x] Prioridade tem **justificativa explícita**.
- [x] Ambiente inclui **navegador + SO**.
- [x] "Esperado × Obtido" deixa a diferença clara.
- [x] Os 3 defeitos reportados cobrem **categorias diferentes**
      (funcional, UX, validação, persistência, etc.)
