# mwm

Automação, integrações e IA aplicada a rotinas contábeis e fiscais.
**Menos trabalho manual. Mais controle da operação.**

Construo sistemas que leem os documentos que a equipe já produz (PDF, Excel, CSV, TXT, XML), conectam
sistemas que não conversam entre si e conferem cada etapa. O trabalho repetitivo sai das mãos das pessoas
sem que se perca o controle do que foi feito.

Portfólio: **[savez-portfolio.vercel.app](https://savez-portfolio.vercel.app)**

---

## Em destaque: Painel de Obrigações Acessórias

Plataforma web que controla as obrigações fiscais de um escritório contábil e **dá baixa sozinha** ao ler
os documentos da equipe. Um agente reconhece cada arquivo pelo conteúdo (declaração, recibo, apuração,
guia, comprovante), e o painel o amarra à obrigação certa e confere o que foi **apurado**, **declarado**,
**cobrado em guia** e **pago**. Em produção desde agosto de 2026; homologado pela gestão em 16/10/2026 e
usado pela equipe desde 22/10/2026.

Números de 30/10/2026:

- **534 empresas ativas**, **45 obrigações** e **cerca de 4.000 competências por mês** num lugar só
- **106.709 arquivos** lidos sem digitação por **22 leitores** de documento fiscal (26/10/2026)
  (DCTFWeb, eSocial, Reinf, SPED, GIA, PGDAS-D, apurações, PER/DCOMP…)
- **100%** dos vencimentos de 09/2026 entregues no fechamento do mês
- **84,9%** das 1.209 competências de 09/2026 comparadas conformes na conferência entre apurado, declarado e pago
- **606.271 XML** de notas indexados (15/09/2026), e o ISS retido decidido pelas notas de cada mês
- Integração com a API do eContador (Alterdata): o que foi publicado e o que o cliente ainda não abriu
- Cadastro de empresa nova automatizado: a empresa aparece no eContador e a ficha abre sozinha; robôs
  consultam inscrição estadual e Simples Nacional, e a gerência aprova com a prova na tela
- **1.912 testes automatizados** e trilha de auditoria de cada mudança

Desenvolvimento assistido por IA (Claude Code e ChatGPT), com especificação, revisão e validação próprias.

`Next.js` `React` `TypeScript` `Prisma` `PostgreSQL` `Node.js` `SQLite` `pdf.js` `Python` `Playwright` `Vercel`

---

## Central de automação: obrigações fiscais, trabalhistas e contábeis

Aplicativo Windows que reúne as rotinas em lote de um escritório contábil em **16 automações em 13 portais
e sistemas** (e-CAC, PGFN, Caixa, Alterdata, eContador, prefeitura e outros): transmissão da DCTFWeb com
importação do MIT, guias de parcelamento (Receita Federal e PGFN), consultas ao Simples Nacional e à
inscrição estadual, relatórios de folha e fichas no Alterdata, procurações e extratos do FGTS, DMS da
prefeitura, comprovantes e situação fiscal do eContador, SPED e apurações sem movimento. As rotinas rodam
por agenda, uma por vez, a partir das planilhas de controle dos setores; cada robô é conferido por SHA-256
antes de rodar, repetir não duplica emissão e o resultado de cada empresa fica registrado, com aviso por
e-mail. Onde o portal exige verificação contra robôs, como o login do gov.br, quem entra é uma pessoa.

Números de 29/10/2026: **9.693 processos** e **13.947 documentos** registrados desde 09/2026; conferência
dos certificados no Conectividade Social de **198 min para 25 s**; leitura dos pagamentos no eContador de
**77 para 4 páginas**; **84.801 linhas de código**, 20.535 delas de testes (26/10/2026).

`C# (.NET)` `Python` `Node.js` `Playwright` `PowerShell` `.NET 10 (FlaUI)` `UI Automation` `APIs Google` `OCR`

---

## Outros projetos

Todos em uso na rotina de um escritório contábil. Os repositórios são privados porque trabalham com dados
de clientes.

| Projeto | O que resolve | Stack |
|---|---|---|
| **Apurações sem movimento** | Cruza a relação de empresas com os documentos de conferência antes de gerar as apurações de ICMS, ISSQN e PIS/COFINS sem movimento. Empresa com pendência é bloqueada com o motivo; arquivo existente nunca é sobrescrito. Desde 10/2026, também roda integrado à central de automação | Python |
| **Faturamento consolidado** | Calcula o faturamento de até 12 competências a partir das apurações de vários sistemas (Alterdata, Sistema JB, PROMOB e outros), consolida matriz e filiais, confere com o balancete e a DRE e gera o demonstrativo em PDF assinado pelo responsável legal, arquivando os documentos usados e enviando tudo por e-mail à contabilidade | Python |
| **Gestão de Extratos Bancários** | Lê a caixa de e-mail central, reconhece os extratos pelo conteúdo, identifica banco, conta, titular e competência, confronta a empresa com o cadastro do mês e arquiva o PDF na rede com nome padronizado, conferindo a cópia por hash e recibo assinado antes de retirar o original do Drive. Separa o documento guardado do pedido do cliente, que fica pendente até alguém responder. Em operação desde 09/2026 | Google Apps Script · Node.js · PowerShell · APIs Google · OCR |
| **SPED Fiscal** | Cálculo do DIFAL e dos ajustes E111/E113 | Python |
| **Ressarcimento de IPI** | Gera os arquivos R11 e R12 para importação no PER/DCOMP Web | Python |
| **Reajuste de Dissídio** | Calcula o dissídio de cada funcionário pelas regras de 8 convenções coletivas (proporcionalidade, piso, teto, horistas e compensação de aumentos lida do PDF de alterações salariais), com conferência antes de gerar, e entrega a planilha do cliente pronta para o retroativo. Em produção desde 07/2026: 670 funcionários de 45 empresas até 19/10/2026 e 55 testes automatizados | Python · tkinter · openpyxl · pdfplumber |
| **Retroativo do dissídio** | Calcula o retroativo a partir da planilha do reajuste e gera o arquivo de importação da folha no Alterdata | Python |
| **Gerador Alterdata (importação do ponto)** | Transforma as planilhas de lançamentos e os espelhos de ponto em PDF dos clientes no TXT de importação do Alterdata, confere código e nome de cada funcionário, memoriza os códigos confirmados e bloqueia formatos ambíguos. Em uso pelo Departamento Pessoal desde 09/2026 | Python · tkinter · SQLite · PyMuPDF |
| **Folha → contabilidade** | Integra os relatórios de folha do Alterdata ao arquivo de importação contábil do Infor | Python |

---

## Como eu trabalho

- **Começo pelo processo real**, não pelo desenho: volume, exceções e onde a rotina trava.
- **Regra determinística onde uma regra resolve; IA só onde gera valor verificável**, com conferência
  humana na decisão final.
- **Meço contra os arquivos de produção** antes de dizer que funciona: reconhecer o documento não prova
  que os valores foram lidos.
- **Documento de cliente não entra no repositório**, nem como exemplo de teste.
- **Tudo idempotente e rastreável**: rodar duas vezes não duplica, e cada mudança registra quem, quando
  e por quê.

---

## Tecnologias

**Linguagens** · TypeScript · JavaScript · Python · C# · SQL · PowerShell<br>
**Web** · Next.js · React · Tailwind CSS · APIs REST<br>
**Dados** · PostgreSQL · Prisma · SQLite · Excel<br>
**Automação e documentos** · Node.js · Playwright · pdf.js · Google Apps Script · OCR · XML<br>
**Entrega** · Git · GitHub · Vercel · Agendador de Tarefas do Windows

---

Tem uma rotina que se repete e trava? **[Conte qual é](https://savez-portfolio.vercel.app/contato)**.
