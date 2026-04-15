# 🚀 Hands-on: Spec Driven Development (SDD) com GitHub Copilot

Bem-vindo! Neste hands-on você vai aprender como usar o GitHub Copilot para desenvolver software seguindo o fluxo:

👉 **Spec → Testes → Código → Refatoração**

---

## 🟢 Início rápido

1. Abra este repositório no Codespaces
2. Aguarde o ambiente iniciar
3. Abra o Copilot Chat
4. Siga as etapas abaixo

---

## 🎯 Objetivo

Ao final deste exercício, você será capaz de:

* Criar uma SPEC clara
* Gerar testes automaticamente com Copilot
* Implementar código guiado por testes
* Entender o fluxo de SDD na prática

---

## ⏱️ Duração

~45 a 60 minutos

---

## 🧰 Pré-requisitos

* Conta no GitHub
* Conhecimento básico de programação
* Noções básicas de Python

---

## 📁 Estrutura do projeto

```
spec/     → requisitos e regras de negócio
tests/    → testes automatizados
src/      → implementação
```

---

## 🧭 Fluxo do exercício

* [ ] Etapa 1 — Criar SPEC
* [ ] Etapa 2 — Gerar TESTES
* [ ] Etapa 3 — Implementar CÓDIGO
* [ ] Etapa 4 — Refatorar

---

# 🧪 Etapa 1 — Criar a SPEC

## 🎯 Objetivo

Definir claramente o comportamento do sistema antes de escrever código.

## 👉 Ação

Abra o Copilot Chat e execute:

```
Crie ou refine a SPEC para um sistema de pedidos com:
- criar pedido
- adicionar itens
- calcular total
- aplicar desconto simples
```

## ✅ Resultado esperado

Arquivo `spec/requirements.md` com regras claras e exemplos.

---

✅ **Checkpoint:** Você criou a SPEC com sucesso!

---

# 🧪 Etapa 2 — Criar os TESTES

## 🎯 Objetivo

Gerar testes baseados na SPEC (sem implementar código ainda).

## 👉 Ação

No Copilot Chat:

```
Gere testes usando pytest baseados exclusivamente na SPEC.
Não implemente a lógica.
```

## ▶️ Execute os testes

```bash
pytest
```

## ❗ Resultado esperado

Os testes devem falhar.

👉 Isso é esperado no SDD.

---

❌ **Checkpoint:** Testes falhando? Perfeito — você está no caminho certo.

---

# 🧪 Etapa 3 — Implementar o CÓDIGO

## 🎯 Objetivo

Implementar o mínimo necessário para passar nos testes.

## 👉 Ação

No Copilot Chat:

```
Implemente o código em src/ para fazer os testes passarem.
```

## ▶️ Execute novamente

```bash
pytest
```

## ✅ Resultado esperado

Todos os testes passando.

---

✅ **Checkpoint:** Testes passando!

---

# 🧪 Etapa 4 — Refatoração

## 🎯 Objetivo

Melhorar o código mantendo os testes verdes.

## 👉 Ação

```
Refatore o código melhorando nomes e organização sem quebrar os testes.
```

---

✅ **Checkpoint:** Código mais limpo e organizado!

---

# 🧠 Conclusão

Você aplicou na prática:

* Spec antes do código
* Testes como contrato
* Copilot como acelerador
* Desenvolvimento guiado por comportamento

---

## 🚀 Próximos passos

* Adicionar API com FastAPI
* Criar pipeline CI no GitHub Actions
* Evoluir regras de negócio

---

## 💡 Dica final

Sempre siga:

❌ Não comece pelo código
✅ Comece pela SPEC

---

## 🏁 Finalização

Se você chegou até aqui:

🎉 Parabéns! Você executou um fluxo completo de Spec Driven Development usando GitHub Copilot.
