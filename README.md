# Proposta de Visualização de Dados do NoFeling

## Visão Geral

O projeto **NoFeling** utiliza algoritmos de grafos para otimizar a seleção de bases operacionais no combate a incêndios florestais. Como parte estratégica desta solução, desenvolvemos uma interface de inteligência geoespacial focada na análise de focos de incêndio no estado do Mato Grosso do Sul.

O **Heatmap de ocorrências por municípios** fornece suporte à tomada de decisão executiva, permitindo a identificação rápida de *hotspots* para uma realocação de recursos mais eficiente e precisa.

---

## Heatmap de Ocorrências e Inteligência Geográfica

### Objetivo e Público-Alvo
Desenvolvido com foco na persona de **Douglas Guedes (Gerente Executivo de Inteligência Patrimonial)**, o mapa oferece uma leitura executiva e interativa da distribuição de incêndios. Ao identificar as regiões com maior densidade de ocorrências, a gestão pode propor estrategicamente novas localizações para bases, equipamentos e equipes.

### Animação e interatividade em D3.js

Para garantir uma experiência fluida e análises mais profundas, a visualização conta com as seguintes implementações avançadas em D3.js:

* **Navegação Espacial (`d3.zoom`):** Implementação de funcionalidades de *pan* e *zoom* integradas ao mapa do Mato Grosso do Sul. Isso permite que o usuário aproxime regiões com alta densidade de bolhas para uma inspeção minuciosa de municípios vizinhos sem perder a resolução.
* **Animação de Entrada (`.transition()`):** Os dados não aparecem de forma abrupta. Utilizamos transições suaves na renderização inicial, onde as bolhas de calor (representando o volume de incêndios) surgem de forma gradativa na tela, facilitando o mapeamento cognitivo da distribuição geográfica.
* **Marcação de Áreas Críticas (`d3.drag` e `d3.quadtree`):** O usuário pode arrastar um "alfinete de atenção" pelo mapa. A funcionalidade de *drag* permite o reposicionamento livre, enquanto a *quadtree* atua nos bastidores para otimizar a performance, fazendo com que o alfinete identifique e se ancore rapidamente às áreas de risco mais próximas durante o movimento.
* **Seleção de Focos (`d3.brush`):** Ferramenta de seleção de área. O gestor pode desenhar um retângulo de destaque (*brush*) sobre uma região específica do mapa para isolar e visualizar instantaneamente o consolidado de ocorrências de incêndio e a área total queimada apenas daquele recorte geográfico.

### Arquitetura e Pipeline de Dados

| Componente       | Detalhe                              |
|------------------|--------------------------------------|
| **Tipo** | Mapa coroplético (heatmap) com sobreposição de bolhas proporcionais e controles interativos. |
| **Fonte de Dados** | Incêndios por UP (`incendios_ups.csv`), localização de fazendas (`Fazendas_MS.csv`), geometrias de MS (GeoJSON / API IBGE). |
| **Tecnologias** | D3.js v7, JavaScript, HTML5 Canvas. |

1. **Processamento:** Integração das coordenadas das Unidades Produtivas com os mapas GeoJSON dos municípios de MS.
2. **Geolocalização (`d3.geoContains`):** Validação de limites municipais para agrupar ocorrências e acumular a área total queimada.
3. **Codificação Visual:** Aplicação de escala de cores quantitativa (saturação baseada no volume de incêndios) e *size encoding* (tamanho das bolhas proporcional à magnitude da área).
4. **Tooltips:** Exibição de dados detalhados (UPs envolvidas, ocorrências e microrregião) em *hover*.

---

### Como rodar

- Baixe a extensão Live Server no VS Code.
- Clique com o botão esquerdo no arquivo `ms-mapa.html` e selecione a opção *Open with Live Server*

---

### Equipe Responsável

* Maria Clara Oliveira
* Messias Olivindo