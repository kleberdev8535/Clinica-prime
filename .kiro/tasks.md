[tasks.md](https://github.com/user-attachments/files/26544219/tasks.md)
# Plano de Implementação — Clínica Sorriso Prime

## Overview

Implementação incremental de um site institucional estático (index.html, style.css, main.js) para a Clínica Sorriso Prime. Cada tarefa produz código funcional e integrado ao passo anterior, sem código órfão.

## Tasks

- [x] 1. Setup do projeto e estrutura base
  - Criar os três arquivos: `index.html`, `style.css`, `main.js` na pasta `Clinica/`
  - Configurar `index.html` com estrutura semântica mínima: `<!DOCTYPE html>`, `<head>` com meta viewport, link para `style.css` e `<script defer src="main.js">`, link Google Fonts (Poppins), link Font Awesome CDN
  - Definir variáveis CSS no `:root` de `style.css`: `--color-white`, `--color-blue`, `--color-green`, `--color-dark`, `--color-gray`, `--font-main`, `--section-py`, `--radius`, `--shadow`
  - Adicionar reset CSS básico e `scroll-behavior: smooth` no elemento `html`
  - Declarar constante `CONFIG` em `main.js` com `whatsappNumber`, `whatsappMessage` e `breakpointMobile`
  - _Requirements: 1.6, 10.1, 10.2, 10.5_

- [x] 2. Menu fixo e navegação
  - [x] 2.1 Implementar `<header>` com `<nav>` fixo no topo em `index.html`
    - Incluir logotipo (texto "Clínica Sorriso Prime") e links âncora para `#hero`, `#sobre`, `#servicos`, `#diferenciais`, `#depoimentos`, `#equipe`, `#contato`
    - Adicionar botão hambúrguer (`<button class="hamburger">`) visível apenas em mobile
    - _Requirements: 1.1, 1.2, 1.3_
  - [x] 2.2 Estilizar menu fixo em `style.css`
    - `position: fixed; top: 0; width: 100%; z-index: 1000`
    - Mobile-first: links ocultos por padrão, exibidos em coluna quando classe `.open` presente
    - Breakpoint 768px: links em linha, hambúrguer oculto
    - _Requirements: 1.3, 1.5, 10.5_
  - [x] 2.3 Implementar `initHamburgerMenu()` em `main.js`
    - Toggle da classe `.open` no `<nav>` ao clicar no botão hambúrguer
    - Fechar menu ao clicar em qualquer link âncora
    - _Requirements: 1.4, 1.5_
  - [ ]* 2.4 Escrever testes de exemplo para menu e navegação
    - Verificar presença do `<header>` com `position: fixed` no CSS
    - Verificar que o nav contém links âncora para todas as 7 seções
    - Verificar presença do botão hambúrguer no DOM
    - _Requirements: 1.2, 1.3, 1.5_

- [x] 3. Seção Hero
  - [x] 3.1 Implementar `<section id="hero">` em `index.html`
    - Título: "Cuide do seu sorriso com especialistas"
    - Subtítulo descritivo sobre qualidade, tecnologia e atendimento humanizado
    - CTA `<a>` com texto "Agendar consulta no WhatsApp" e `href` gerado via `buildWhatsAppUrl()`
    - Imagem de fundo via CSS com overlay de cor para legibilidade
    - _Requirements: 2.1, 2.2, 2.3, 2.4_
  - [x] 3.2 Implementar `buildWhatsAppUrl(msg)` em `main.js`
    - Retorna `https://wa.me/{CONFIG.whatsappNumber}?text={encodeURIComponent(msg)}`
    - Atualizar `href` do CTA Hero ao inicializar
    - _Requirements: 2.3, 9.2_
  - [x] 3.3 Estilizar seção Hero em `style.css`
    - Background com overlay, tipografia responsiva, padding mínimo de 60px vertical
    - Ajuste de font-size em mobile (<768px)
    - _Requirements: 2.4, 2.5, 10.3_
  - [ ]* 3.4 Escrever teste de propriedade — Property 1: Links de WhatsApp são URLs válidas com mensagem
    - **Property 1: Links de WhatsApp são URLs válidas com mensagem**
    - **Validates: Requirements 2.3, 8.1, 9.2**
    - Usar `fc.constantFrom(...whatsappLinks)` para iterar sobre todos os CTAs WhatsApp do DOM
    - Verificar `url.hostname === 'wa.me'` e `url.searchParams.get('text').length > 0`
    - Mínimo 100 iterações (`numRuns: 100`)

- [x] 4. Seção Sobre
  - [x] 4.1 Implementar `<section id="sobre">` em `index.html`
    - Texto institucional sobre qualidade, tecnologia e atendimento humanizado
    - Ao menos 3 cards de destaque com ícone FA, número/estatística e rótulo (ex.: "15+ Anos de Experiência", "5000+ Pacientes", "10 Especialistas")
    - _Requirements: 3.1, 3.2_
  - [x] 4.2 Estilizar seção Sobre em `style.css`
    - Cards em coluna única no mobile, grid de 3 colunas em ≥768px
    - Padding vertical mínimo de 60px
    - _Requirements: 3.3, 10.3_
  - [ ]* 4.3 Escrever teste de propriedade — Property 5: Seção Sobre exibe ao menos três itens de destaque
    - **Property 5: Seção Sobre exibe ao menos três itens de destaque**
    - **Validates: Requirements 3.2**
    - Verificar que `document.querySelectorAll('#sobre .highlight-item').length >= 3`

- [x] 5. Seção Serviços
  - [x] 5.1 Implementar `<section id="servicos">` em `index.html`
    - 4 cards: Limpeza Dentária, Clareamento, Implantes, Ortodontia
    - Cada card: `<i>` com classe Font Awesome, `<h3>` com nome, `<p>` com descrição (até 2 frases)
    - _Requirements: 4.1, 4.2_
  - [x] 5.2 Estilizar seção Serviços em `style.css`
    - Mobile: coluna única; ≥768px: grid de 2 colunas; ≥1024px: grid de 4 colunas
    - Padding vertical mínimo de 60px
    - _Requirements: 4.3, 4.4, 10.3_
  - [ ]* 5.3 Escrever teste de propriedade — Property 2: Cards de conteúdo contêm ícone, título e descrição
    - **Property 2: Cards de conteúdo contêm ícone, título e descrição**
    - **Validates: Requirements 4.2, 5.2**
    - Usar `fc.constantFrom(...serviceCards, ...differentialCards)` para iterar sobre todos os cards
    - Verificar presença de `<i>`, elemento de título com texto não vazio e `<p>` com texto não vazio

- [x] 6. Seção Diferenciais
  - [x] 6.1 Implementar `<section id="diferenciais">` em `index.html`
    - 4 cards: Atendimento Personalizado, Tecnologia Moderna, Profissionais Qualificados, Ambiente Confortável
    - Cada card: `<i>` com classe FA, `<h3>` com título, `<p>` com descrição curta
    - _Requirements: 5.1, 5.2_
  - [x] 6.2 Estilizar seção Diferenciais em `style.css`
    - Mobile: coluna única; ≥768px: grid de 2 colunas; ≥1024px: grid de 4 colunas
    - Padding vertical mínimo de 60px
    - _Requirements: 5.3, 10.3_

- [x] 7. Checkpoint — Verificar estrutura e testes das seções iniciais
  - Garantir que todos os testes passam até este ponto, perguntar ao usuário se houver dúvidas.

- [x] 8. Seção Depoimentos
  - [x] 8.1 Implementar `<section id="depoimentos">` em `index.html`
    - 3 cards fictícios, cada um com: nome do paciente, texto do depoimento, 4 ou 5 elementos `<span class="star">` representando estrelas
    - _Requirements: 6.1, 6.2_
  - [x] 8.2 Estilizar seção Depoimentos em `style.css`
    - Cards com fundo diferenciado (`--color-gray`), mobile: coluna única, ≥768px: grid de 3 colunas
    - Padding vertical mínimo de 60px
    - _Requirements: 6.2, 6.3, 10.3_
  - [ ]* 8.3 Escrever teste de propriedade — Property 3: Seção Depoimentos tem cardinalidade e estrutura corretas
    - **Property 3: Seção Depoimentos tem cardinalidade e estrutura corretas**
    - **Validates: Requirements 6.1**
    - Verificar `cards.length >= 2 && cards.length <= 3`
    - Para cada card: nome não vazio, texto não vazio, `2 <= stars <= 5` e `stars >= 4`

- [x] 9. Seção Equipe
  - [x] 9.1 Implementar `<section id="equipe">` em `index.html`
    - 3 cards fictícios, cada um com: `<img>` circular com `src` placeholder e `alt` descritivo, `<h3>` com nome completo, `<p>` com especialidade
    - _Requirements: 7.1_
  - [x] 9.2 Estilizar seção Equipe em `style.css`
    - `<img>` com `border-radius: 50%`, `background-color` de fallback
    - Mobile: coluna única; ≥768px: flex em linha
    - Padding vertical mínimo de 60px
    - _Requirements: 7.2, 7.3, 10.3_
  - [ ]* 9.3 Escrever teste de propriedade — Property 4: Seção Equipe tem cardinalidade e estrutura corretas
    - **Property 4: Seção Equipe tem cardinalidade e estrutura corretas**
    - **Validates: Requirements 7.1**
    - Verificar `cards.length >= 2 && cards.length <= 3`
    - Para cada card: `img.src` não vazio, nome não vazio, especialidade não vazia

- [x] 10. Seção Contato e Botão Flutuante
  - [x] 10.1 Implementar `<section id="contato">` em `index.html`
    - CTA `<a>` "Falar no WhatsApp" com `href` via `buildWhatsAppUrl()`
    - Telefone fictício e endereço fictício
    - `<iframe>` do Google Maps apontando para endereço fictício
    - _Requirements: 8.1, 8.2, 8.3, 8.4_
  - [x] 10.2 Implementar botão flutuante em `index.html`
    - `<a class="whatsapp-float">` fixo no canto inferior direito com ícone FA do WhatsApp
    - `href` via `buildWhatsAppUrl()` definido em `main.js` na inicialização
    - _Requirements: 9.1, 9.2, 9.4_
  - [x] 10.3 Estilizar seção Contato e botão flutuante em `style.css`
    - Contato: mobile empilhado, ≥768px lado a lado; padding mínimo 60px
    - Botão flutuante: `position: fixed; bottom: 24px; right: 24px; width: 56px; height: 56px; border-radius: 50%; z-index: 999`
    - _Requirements: 8.5, 9.1, 9.3, 10.3_
  - [ ]* 10.4 Escrever testes de exemplo para Contato e Botão Flutuante
    - Verificar presença do `<iframe>` na seção `#contato`
    - Verificar que `.whatsapp-float` existe no DOM
    - Verificar que o CSS define `position: fixed` e dimensões mínimas de 56x56px para `.whatsapp-float`
    - _Requirements: 8.4, 9.1, 9.3_

- [x] 11. Rodapé
  - [x] 11.1 Implementar `<footer>` em `index.html`
    - Nome da clínica, links de navegação rápida, `<span id="copyright-year">` para o ano
    - _Requirements: 11.1_
  - [x] 11.2 Implementar atualização dinâmica do ano em `main.js`
    - `document.getElementById('copyright-year').textContent = new Date().getFullYear()`
    - _Requirements: 11.1_
  - [x] 11.3 Estilizar rodapé em `style.css`
    - Mobile: elementos empilhados; ≥768px: flex em linha
    - _Requirements: 11.2_
  - [ ]* 11.4 Escrever teste de propriedade — Property 7: Copyright exibe o ano atual
    - **Property 7: Copyright exibe o ano atual**
    - **Validates: Requirements 11.1**
    - Verificar que o texto do rodapé contém `new Date().getFullYear().toString()`

- [x] 12. Estilo global e responsividade final
  - [x] 12.1 Revisar e completar media queries em `style.css`
    - Garantir breakpoints `@media (min-width: 768px)` e `@media (min-width: 1024px)` presentes e cobrindo todas as seções
    - _Requirements: 10.5_
  - [x] 12.2 Implementar `initSmoothScroll()` em `main.js`
    - Fallback JS para scroll suave em browsers que não suportam `scroll-behavior: smooth`
    - _Requirements: 1.4_
  - [ ]* 12.3 Escrever testes de exemplo para CSS global
    - Verificar que variáveis `--color-blue`, `--color-green`, `--color-white` estão definidas no `:root`
    - Verificar que media queries para 768px e 1024px estão presentes no CSS
    - _Requirements: 10.1, 10.5_
  - [ ]* 12.4 Escrever teste de propriedade — Property 6: Todas as seções têm padding vertical mínimo de 60px
    - **Property 6: Todas as seções têm padding vertical mínimo de 60px**
    - **Validates: Requirements 10.3**
    - Usar `fc.constantFrom(...sections)` para iterar sobre todas as `<section>`
    - Verificar que `--section-py` está definido como `60px` e aplicado a todas as seções

- [x] 13. Checkpoint final — Garantir que todos os testes passam
  - Garantir que todos os testes passam, perguntar ao usuário se houver dúvidas.

## Notes

- Tarefas marcadas com `*` são opcionais e podem ser puladas para um MVP mais rápido
- Cada tarefa referencia requisitos específicos para rastreabilidade
- Os testes usam Jest + jsdom para testes de exemplo e fast-check para testes de propriedade
- O produto final são três arquivos estáticos em `Clinica/`: `index.html`, `style.css`, `main.js`
