# CLAUDE.md

## Este repositório (agendamento-exames)

Página estática (single-file, `index.html`) de agendamento de exames ocupacionais do
DETRAN-RR, publicada no Render em `agendamento.protecaorr.net`. Backend 100% Supabase,
sem build. Ver `README.md`.

## Projeto Auditor Proteção RR (esocial.protecaorr.net)

Contexto do produto: ver @HANDOFF_AUDITOR_ESOCIAL.md

Plano de implementação da Fase 1: ver @PLANO_FASE_1_AUDITOR.md

> Domínio definido pelo Haroldo em 06/10/2026: **esocial.protecaorr.net** (o handoff
> cita "auditor.protecaorr.net", que foi substituído). A página provisória "em
> construção" está em `esocial/index.html`, publicada como segundo site estático no
> Render. O auditor terá repositório próprio quando a Fase 1 começar de fato; o
> handoff e o plano estão aqui provisoriamente porque este é o único repositório
> existente da conta.

### Regras do projeto Auditor
- eSocial Brasil é só referência funcional — não copiar código, layout, textos ou marca.
- Modelo de dados segue os leiautes oficiais do eSocial S-1.3 e o MOS, não o sistema analisado.
- LGPD: nunca usar dados pessoais reais de trabalhadores em seeds, fixtures ou logs.
