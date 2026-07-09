# Guia de Interação — Próximos Passos do Painel IBDM

Guia prático para executar o blueprint da skill `site-ibdm-4conf-builder` no Claude Code, na ordem certa. Cada bloco tem um prompt pronto para copiar e colar, e um marcador quando a ação é sua (fora do Claude).

## Antes de começar

1. Abra o Claude Code (desktop, terminal ou app) e clone o repositório:
   ```
   git clone https://github.com/vitorms-adv/ibdm_4conf.git
   cd ibdm_4conf
   ```
2. Garanta que a skill `site-ibdm-4conf-builder` está salva no seu perfil (clique em "Salvar skill" no cartão do arquivo, se ainda não fez) — assim ela carrega automaticamente quando você mencionar o painel do IBDM, sem precisar reexplicar nada.

## 🔧 Passo 1 — Ajustes na planilha (ação sua, no Google Sheets)
Antes de mexer em código, ajuste a planilha você mesmo:
- Confirme/crie as colunas da aba Logística (nome, subcategoria, responsável, fornecedor, status, valor previsto, valor executado, prazo, conclusão).
- Adicione a coluna de status Aprovado/Planejado nas linhas já existentes de Receita/Despesa do Financeiro.

## 💻 Passo 2 — Backend (Apps Script)
Prompt:
> "Usando a skill site-ibdm-4conf-builder, crie o Code.gs do Apps Script com os endpoints de leitura/escrita por módulo e a validação de senha no backend."

**Ação sua**: dentro da planilha, Extensões → Apps Script → colar o código gerado → Implantar → Nova implantação → Aplicativo da Web. Guarde a URL gerada, você vai usá-la no próximo passo.

## 💻 Passo 3 — Limpeza do frontend
Prompt:
> "Remova do index.html o Gantt de Marcos Críticos e todo o CSS morto associado (.marcos-timeline, .marco-dot)."

## 💻 Passo 4 — Trocar CSV pelo Apps Script
Prompt:
> "Troque as chamadas de fetch ao CSV publicado pelas chamadas ao endpoint do Apps Script: [cole aqui a URL do Passo 2]."

## 💻 Passo 5 — Gate de senha
Prompt:
> "Implemente a tela de bloqueio por senha única, validada no backend, sem opção de lembrar o aparelho."

## 💻 Passo 6 — Módulo Logística
Prompt:
> "Construa o módulo de Logística completo: listagem, modal de Adicionar/Editar, soft delete (arquivar) e filtros por subcategoria/status."

**Checkpoint**: teste adicionar, editar e arquivar um item de teste antes de seguir.

## 💻 Passo 7 — CRUD nos módulos existentes
Prompt:
> "Aplique o mesmo padrão de modal + soft delete nos módulos Agraciados, Palestrantes, Patrocinadores, Programação, Financeiro e Banco de Palestrantes."

## 💻 Passo 8 — Índice de Prontidão + espaço do Gantt
Prompt:
> "Recalcule o Índice de Prontidão com os novos pesos (Agraciados 31,25%, Palestrantes 31,25%, Patrocinadores 25%, Captação financeira 12,5%) e ocupe o espaço do antigo Gantt com um resumo do módulo Logística."

## 💻 Passo 9 — Integração Logística → Financeiro
Prompt:
> "Implemente no backend a soma automática dos itens de Logística com status Aprovado ou Pago às despesas do Financeiro."

## 🎨 Passo 10 — Identidade visual
Prompt:
> "Aplique a identidade visual do IBDM: paleta azul-marinho + dourado, e o brasão no cabeçalho do painel."

## ✅ Passo 11 — Teste final
Prompt:
> "Rode um checklist de teste ponta a ponta: login por senha, CRUD com soft delete em cada módulo, cálculo do Índice de Prontidão, e a integração Logística-Financeiro."

## Dica de segurança no processo
Faça `git commit` ao final de cada passo com código (2 a 10), não só no final — se algo quebrar num passo, você volta pro commit anterior sem perder o restante do trabalho.
