# Estrutura de referência — eSocial Brasil (clinica.esocialbrasil.com.br)

Mapeamento da estrutura do sistema eSocial Brasil para servir de **base de
inspiração** ao nosso sistema (agendamento-exames → plataforma SST da
Proteção RR). Levantado a partir da navegação nas telas (prints) e do uso
diário do sistema. Não copiamos código nem identidade visual — apenas a
organização de funcionalidades e o modelo de dados implícito.

> Status: em construção. Seções marcadas com ❓ aguardam prints das telas.

## 1. Visão geral

Sistema multiempresa de gestão de SST para clínicas/consultorias. A conta da
consultoria (ex.: 558 - PROTECAO RR) administra N empresas-cliente, e cada
empresa concentra empregados, exames (ASO), treinamentos, EPIs, documentos e
programas (PGR, PCMSO etc.). Tudo alimenta um motor de **vencimentos**.

Plano limita a conta por nº de empregados (ex.: 1085 de 2000 usados).

## 2. Menu lateral (estrutura observada)

| Menu | O que faz (observado/inferido) | Confirmado? |
|---|---|---|
| Central de Ajuda | Base de conhecimento | ✔ (visto no menu) |
| Dashboard | Cartões: Empresas Ativas, Empregados, Turmas Criadas, Total ASOs; gráfico mensal EPIs × Exames × Treinamentos; painel Gestão de Vencimentos (por colaborador e por ações/programas), contagem de vencidos e "empresas impactadas" | ✔ (print 06/10) |
| Empresas | Listagem "Empresas que administro": filtros (nome, tipo, situação), busca, Exportar; ações **+ Nova Empresa** (dropdown), **Importar** (lote), **Demissão em Lote**; colunas ID, empresa (fantasia + razão + CNPJ/CPF), filiais, nº empregados, data de inclusão, situação (Liberado/Bloqueado), Acessar | ✔ (print 06/10) |
| Documentos | ❓ submenus | ❓ |
| Treinamentos | Turmas (81 criadas), certificados? | ❓ |
| Medicina | ASO, exames, PCMSO? (3060 ASOs emitidos) | ❓ |
| Drive | Arquivos por empresa? | ❓ |
| Relatórios | ❓ | ❓ |
| Gestão de Vencimentos | Painel de prazos: EPIs, Exames, Treinamentos por colaborador; PGR, AEP, AET, PCA, PCMSO, Checklist, Psicossocial por empresa | ✔ (dashboard) |
| API de Integração | Cadastros via API (automação) | ✔ (visto no menu) |
| Financeiro | Cobrança das empresas (liga com situação Bloqueado?) | ❓ |
| Catálogo de Riscos | Riscos ocupacionais p/ PGR/PPP | ❓ |
| Gerenciar Cadastro | ❓ | ❓ |
| Usuários | Usuários da conta consultoria | ❓ |
| Permissões | Perfis de acesso | ❓ |
| Configurações | ❓ | ❓ |

## 3. Conceitos-chave do modelo de dados (inferido)

- **Conta/Consultoria** (tenant) → tem plano com limite de empregados.
- **Empresa** (cliente da consultoria): nome fantasia, razão social,
  CNPJ **ou** CPF (produtor rural PF), matriz/filiais, situação
  (Liberado/Bloqueado — possivelmente ligada ao financeiro), data de inclusão.
- **Empregado**: pertence a uma empresa; consome cota do plano.
- **ASO/Exame**: por empregado, com validade → vencimentos.
- **Treinamento**: turmas; certificado por empregado, com validade.
- **EPI**: entrega por empregado, com validade (CA).
- **Programas** (por empresa): PGR, AEP, AET, PCA, PCMSO, Checklist,
  Psicossocial — todos com vigência → vencimentos.
- **Vencimento**: entidade transversal (o "motor" do sistema): tudo que tem
  validade aparece no painel com janelas Hoje / Semana / N dias.

## 4. Fluxo de cadastro de empresas

❓ Aguardando prints do dropdown **+ Nova Empresa** e do formulário.
Observado até aqui: cadastro individual (dropdown com opções) e importação
em lote; suporte a filiais; aceita CNPJ e CPF.

## 5. O que levar para o nosso sistema (proposta inicial)

Hoje o agendamento-exames tem: agendamento público por CPF + painel do
gestor (Agendamentos, Servidores, Agenda) no Supabase. Evolução sugerida,
por fases:

1. **Fase 1 — Multiempresa:** tabela `empresas` (razão social, fantasia,
   cnpj_cpf, situação, data_inclusao) e vincular servidores/empregados a
   uma empresa. Tela de listagem com busca/filtros, nos moldes da
   "Empresas que administro".
2. **Fase 2 — Validades:** dar validade ao exame/ASO agendado e criar o
   painel de vencimentos (Hoje / Semana / 30 dias), que é o maior valor
   percebido do sistema de referência.
3. **Fase 3 — Módulos:** treinamentos e EPIs com o mesmo padrão de
   validade; documentos por empresa (storage do Supabase).
4. **Fase 4 — Relatórios/da­shboard:** cartões e gráfico mensal
   (exames realizados × vencidos).

## 6. Pendências de levantamento (prints a coletar)

- [ ] Dropdown **+ Nova Empresa** e formulário completo de cadastro
- [ ] Dropdown **Importar** (modelo de planilha?)
- [ ] Tela interna de uma empresa (após "Acessar")
- [ ] Submenus: Documentos, Treinamentos, Medicina
- [ ] Tela Gestão de Vencimentos (completa)
- [ ] Tela API de Integração (endpoints disponíveis?)
