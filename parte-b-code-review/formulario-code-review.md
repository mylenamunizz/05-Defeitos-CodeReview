# 🔎 Formulário — Parte B

> Preencha uma seção por finding. O mínimo esperado é **6 findings**.

**Dupla:** Ana Karolina Moura. 229033. + Mylena Muniz Jacob. 227488.
**Data da revisão:** 23/04/2026.

---

### Finding #1

**📍 Linha(s):** 12/13.
**🏷 Rótulo:** blocker.
**📂 Dimensão:** Segurança.
**⚠️ Severidade:** Crítica.

**🐛 Problema:** A função buscarUsuarioPorNome concatena diretamente o parâmetro nome na query SQL, permitindo SQL Injection. Um atacante pode passar ' OR '1'='1 e retornar todos os registros do banco.

**💡 Sugestão de correção:** 
async function buscarUsuarioPorNome(nome) {
  return db.executarQuery('SELECT * FROM usuarios WHERE nome = ?', [nome]);
}


### Finding #2

**📍 Linha(s):** 20.
**🏷 Rótulo:** blocker.
**📂 Dimensão:** Segurança.
**⚠️ Severidade:** Crítica.

**🐛 Problema:** O campo tipo é persistido no banco sem nenhuma validação, mesmo existindo a constante TIPOS_VALIDOS declarada no arquivo. Valores arbitrários como "admin" ou "superuser" poderiam ser inseridos sem restrição.

**💡 Sugestão de correção:**
if (!TIPOS_VALIDOS.includes(dados.tipo)) {
  throw new Error(`Tipo inválido. Valores aceitos: ${TIPOS_VALIDOS.join(', ')}`);
}

### Finding #3

**📍 Linha(s):** 26.
**🏷 Rótulo:** major.
**📂 Dimensão:** Segurança.
**⚠️ Severidade:** Alta.

**🐛 Problema:** O objeto usuario retornado por cadastrarUsuario inclui o campo senha (mesmo que hasheado). Expor o hash em respostas é uma má prática de segurança, pois facilita ataques de força bruta offline caso o dado seja interceptado ou logado.

**💡 Sugestão de correção:**
const { senha, ...usuarioSemSenha } = usuario;
return usuarioSemSenha;


### Finding #4

**📍 Linha(s):** 32-35.
**🏷 Rótulo:** blocker.
**📂 Dimensão:** Erros.
**⚠️ Severidade:** Alta.

**🐛 Problema:** A função atualizarEmail não trata o caso em que buscarPorId retorna null ou undefined. Se o id não existir no banco, a linha u.email = novoEmail lançará TypeError: Cannot set properties of null, quebrando a aplicação. Além disso, não há validação de formato do novoEmail.

**💡 Sugestão de correção:** 
async function atualizarEmail(id, novoEmail) {
  const u = await db.buscarPorId('usuarios', id);
  if (!u) throw new Error('Usuário não encontrado');
  if (!novoEmail || !novoEmail.includes('@')) throw new Error('Email inválido');
  u.email = novoEmail;
  await db.atualizar('usuarios', id, u);
  logger.info('Email atualizado: ' + novoEmail);
  return u;
}


### Finding #5

**📍 Linha(s):** 43
**🏷 Rótulo:** nit.
**📂 Dimensão:** Legibilidade.
**⚠️ Severidade:** Baixa.

**🐛 Problema:** A variável hoje é declarada no início de calcularLimiteEmprestimo, mas só é utilizada no bloco final de verificação de bloqueadoAte. Isso cria a falsa impressão de que a data atual influencia toda a lógica da função, prejudicando a legibilidade

**💡 Sugestão de correção:**
// Mover a declaração para próximo do único bloco que a utiliza
if (usuario.bloqueadoAte) {
  const hoje = new Date();
  if (new Date(usuario.bloqueadoAte) > hoje) return 0;
}


### Finding #6

**📍 Linha(s):** 43–100 vs. 103–105
**🏷 Rótulo:** Major.
**📂 Dimensão:** Complexidade.
**⚠️ Severidade:** Média.

**🐛 Problema:** A verificação de bloqueadoAte ocorre ao final de calcularLimiteEmprestimo, após toda a lógica de cálculo ser executada desnecessariamente. Isso é inconsistente com calcularLimiteComSuspensao, que verifica a suspensão logo no início da função, e representa desperdício de processamento e risco de comportamento inesperado.

**💡 Sugestão de correção:**
function calcularLimiteEmprestimo(usuario) {
  // Verificação antecipada, igual ao padrão de calcularLimiteComSuspensao
  if (usuario.bloqueadoAte && new Date(usuario.bloqueadoAte) > new Date()) {
    return 0;
  }

  let limite = 5;
  // ... restante da lógica
}


## ✅ Checklist final

- [X] Há pelo menos 6 findings preenchidas
- [X] Cada finding cita linha, dimensão, rótulo e severidade
- [X] As sugestões são concretas e acionáveis
- [X] Pelo menos uma finding cobre segurança
- [X] Pelo menos uma finding cobre complexidade
