# Novas Casas - Bru & Tha

## O que é
Página estática no GitHub Pages para Bruno e Thaís (esposa) avaliarem casas para alugar juntos. Hospedada em GitHub Pages com dados compartilhados via GitHub API.

## URLs
- **Site:** https://brunext3.github.io/novas-casas/
- **Repo:** https://github.com/BrunexT3/novas-casas (público)
- **Branch:** main

## Arquitetura

### Arquivos
- `index.html` - Página completa (HTML + CSS + JS, tudo inline)
- `data.json` - Dados compartilhados (notas, comentários, status, edições de valores)

### Como funciona o storage
- **Casas (array CASAS):** Hardcoded no HTML. Eu (Claude) adiciono novos cards editando o array e fazendo push.
- **Dados editáveis (data.json):** Salvo no repo via GitHub Contents API. Contém por casa: rating, comments, status (favorita/visitada/descartada), e overrides de valores (preco, condominio, iptu, quartos, banheiros, vagas, area, obs).
- **Overrides:** Valores editados pelo site têm prioridade sobre os hardcoded no array CASAS.
- **Token GitHub:** Fine-grained PAT com permissão Contents (Read/Write) apenas no repo novas-casas. Armazenado no localStorage de cada navegador. NUNCA salvar token no código ou neste chat.

### Fluxo de adição de casas
1. Bruno manda um link de anúncio (VivaReal, Zap, etc.)
2. Eu tento extrair dados via fetch (VivaReal bloqueia scraping - extraio da URL)
3. Adiciono entrada no array CASAS no index.html
4. Commit + push
5. Bruno/Tha complementam dados pelo botão "Editar" no site

## Funcionalidades do site

### Cards
- Foto (ou placeholder), preço aluguel/mês, condomínio, IPTU
- Endereço, quartos, banheiros, vagas, área m²
- Observações (campo livre)
- Link para o anúncio original
- Data de inclusão

### Interações (salvas no data.json compartilhado)
- **Status:** Favorita (amarelo), Visitada (verde), Descartada (cinza/opaco)
- **Nota:** 0-5 estrelas
- **Comentários:** Com seletor de autor (Bru / Tha), data/hora, deletável
- **Editar:** Painel para alterar aluguel, condomínio, IPTU, área, quartos, banheiros, vagas, obs

### Filtros
- Ordenar: mais recentes, mais antigas, menor preço, maior preço, melhor nota
- Status: todas, sem status, favoritas, visitadas, descartadas
- Busca por bairro

## Design
- Tema claro, moderno
- Font: Inter (Google Fonts)
- Header hero com gradiente roxo + animação glow
- Cards com animações fade/scale, hover com elevação
- Ícones SVG inline (pin, bed, bath, car, area, external link)
- Responsivo (mobile-first, 1 coluna em telas < 600px)
- Título: "Casas para Alugar" / subtítulo: "Bru & Tha"

## Casas cadastradas (2026-03-24)

Todas de Sorocaba/SP, condomínios fechados. Foco é **aluguel**.

| ID | Local | Aluguel | Cond | Área | Quartos |
|----|-------|---------|------|------|---------|
| casa-001 | Parque Ibiti Reserva | A consultar (venda R$1.7M) | - | 270m² | 4 |
| casa-002 | Ibiti Royal Park | R$ 8.800 | - | 250m² | 3 |
| casa-003 | Cond. Terras de São Lucas | A consultar (venda R$2.29M) | - | 371m² | 3 |
| casa-004 | Cond. Ibiti Reserva | A consultar (venda R$1.75M) | - | 260m² | 3 |
| casa-005 | Ibiti Royal Park | R$ 10.500 | R$ 480 | 270m² | 4 |
| casa-006 | Cajuru do Sul | R$ 10.000 | - | 350m² | 4 |

**Nota:** Banheiros e vagas não foram extraídos da URL (VivaReal bloqueia scraping). Bruno pode editar pelo site.

## Fonte original dos links
Documento: `F:\Claude-Projetos\Bruno-Workspace\pessoal\casa\Casa Alugel\Casas Para Alugar.docx`

## Pendências
- Bruno precisa criar novo token (o anterior foi exposto no chat e deve ser revogado)
- 3 casas ainda sem valor de aluguel (casa-001, casa-003, casa-004) - Bruno pode editar pelo site
- Sem fotos (VivaReal bloqueia scraping de imagens)
- Considerar: se quiser fotos, Bruno pode fazer upload manual ou colar URL de imagem

## Convenções
- IDs sequenciais: casa-001, casa-002, etc. Próximo: casa-007
- Novos cards adicionados no TOPO do array CASAS
- Commit messages em português
- Git user: BrunexT3 / bruno.dm28@gmail.com
