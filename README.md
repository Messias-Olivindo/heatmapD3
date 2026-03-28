# Proposta de Visualização de Dados do NoFeling

## Visão Geral

O projeto **NoFeling** utiliza algoritmos de grafos para otimizar a seleção de bases operacionais no combate a incêndios florestais. Como parte estratégica desta solução, desenvolvemos uma interface de inteligência geoespacial focada na análise de focos de incêndio no estado do Mato Grosso do Sul.

O **Heatmap de ocorrências por municípios** fornece suporte à tomada de decisão executiva, permitindo a identificação rápida de _hotspots_ para uma realocação de recursos mais eficiente e precisa.

---

## Heatmap de Ocorrências e Inteligência Geográfica

### Objetivo e Público-Alvo

Desenvolvido com foco na persona de **Douglas Guedes (Gerente Executivo de Inteligência Patrimonial)**, o mapa oferece uma leitura executiva e interativa da distribuição de incêndios. Ao identificar as regiões com maior densidade de ocorrências, a gestão pode propor estrategicamente novas localizações para bases, equipamentos e equipes.

### Animação e interatividade em D3.js

Para garantir uma experiência fluida e análises mais profundas, a visualização conta com as seguintes implementações avançadas em D3.js:

- **Navegação Espacial (`d3.zoom`):** Implementação de funcionalidades de _pan_ e _zoom_ integradas ao mapa do Mato Grosso do Sul. Isso permite que o usuário aproxime regiões com alta densidade de bolhas para uma inspeção minuciosa de municípios vizinhos sem perder a resolução.
- **Animação de Entrada (`.transition()`):** Os dados não aparecem de forma abrupta. Utilizamos transições suaves na renderização inicial, onde as bolhas de calor (representando o volume de incêndios) surgem de forma gradativa na tela, facilitando o mapeamento cognitivo da distribuição geográfica.
- **Destaque Dinâmico da Legenda (`hover` + escala proporcional):** Ao passar o mouse sobre uma bolha de ocorrência, a legenda de tamanhos se destaca automaticamente no valor mais próximo daquela área/volume. Esse realce visual ajuda a interpretar rapidamente a magnitude do foco em relação à escala geral do mapa.
- **Marcação de Áreas Críticas (drag-and-drop + `d3.quadtree`):** O usuário pode arrastar o emoji 📍 da legenda e soltá-lo no mapa para criar marcações múltiplas. A `quadtree` ancora rapidamente cada alfinete no foco mais próximo, e cada marcação pode ser removida individualmente pelo botão `x`.

### Arquitetura e Pipeline de Dados

| Componente         | Detalhe                                                                                                                     |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------- |
| **Tipo**           | Mapa coroplético (heatmap) com sobreposição de bolhas proporcionais e controles interativos.                                |
| **Fonte de Dados** | Incêndios por UP (`incendios_ups.csv`), localização de fazendas (`Fazendas_MS.csv`), geometrias de MS (GeoJSON / API IBGE). |
| **Tecnologias**    | D3.js v7, JavaScript, HTML5 Canvas.                                                                                         |

1. **Processamento:** Integração das coordenadas das Unidades Produtivas com os mapas GeoJSON dos municípios de MS.
2. **Geolocalização (`d3.geoContains`):** Validação de limites municipais para agrupar ocorrências e acumular a área total queimada.
3. **Codificação Visual:** Aplicação de escala de cores quantitativa (saturação baseada no volume de incêndios) e _size encoding_ (tamanho das bolhas proporcional à magnitude da área).
4. **Tooltips:** Exibição de dados detalhados (UPs envolvidas, ocorrências e microrregião) em _hover_.

---

### Como rodar

- Baixe a extensão Live Server no VS Code.
- Clique com o botão esquerdo no arquivo `ms-mapa.html` e selecione a opção _Open with Live Server_

---

### Equipe Responsável

- Maria Clara Oliveira
- Messias Olivindo
