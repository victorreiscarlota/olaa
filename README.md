
### Explicação do Código

Este código implementa classes para a manipulação de **grafos** usando diferentes representações (lista de adjacência, matriz de adjacência e matriz de incidência) e inclui algoritmos fundamentais em teoria dos grafos. Aqui está a explicação detalhada de cada método:

---

### **Classes de Representação**
1. **`ListaAdjacencia`**
   - **O que faz:** Representa o grafo como uma lista de adjacências, armazenando os vértices vizinhos para cada vértice.
   - **Métodos principais:**
     - **`adicionar_aresta`:** Adiciona uma aresta ao grafo. Em grafos não-dirigidos, adiciona a aresta em ambos os sentidos. Custo: \(O(1)\) (amortizado) para adicionar uma aresta.
     - **`remover_aresta`:** Remove a aresta se existir. Utiliza list comprehension. Custo: \(O(\deg(u))\), onde \(\deg(u)\) é o grau do vértice \(u\).
     - **`checar_adjacencia`:** Verifica se existe uma aresta entre dois vértices. Custo: \(O(\deg(u))\).
     - **Uso:** Eficiência para grafos esparsos, pois armazena apenas arestas existentes.

2. **`MatrizAdjacencia`**
   - **O que faz:** Representa o grafo como uma matriz \(n 	imes n\), onde \(n\) é o número de vértices. Cada célula indica a presença de uma aresta (e.g., 0 ou peso).
   - **Métodos principais:**
     - **`adicionar_aresta`:** Adiciona uma aresta, modificando as células \(u, v\) (e \(v, u\) se não-dirigido). Custo: \(O(1)\).
     - **`remover_aresta`:** Remove uma aresta, zerando as células. Custo: \(O(1)\).
     - **`checar_adjacencia`:** Verifica se \(M[u][v] 
eq 0\). Custo: \(O(1)\).
   - **Uso:** Ideal para grafos densos, pois facilita o acesso a qualquer aresta.

3. **`MatrizIncidencia`**
   - **O que faz:** Representa o grafo como uma matriz \(n 	imes m\), onde \(n\) é o número de vértices e \(m\) o número de arestas. Cada coluna representa uma aresta.
   - **Métodos principais:**
     - **`adicionar_aresta`:** Adiciona uma coluna na matriz e associa os vértices da aresta. Custo: \(O(n)\) (adicionar coluna).
     - **`remover_aresta`:** Remove a coluna associada à aresta. Custo: \(O(n)\).
     - **`checar_adjacencia`:** Verifica se dois vértices compartilham uma coluna. Custo: \(O(m)\).
   - **Uso:** Mais eficiente em grafos com menos vértices e muitas arestas.

---

### **Classe `Grafo`**
- **Função principal:** Integra as três representações e fornece métodos de análise e manipulação.
- **Destaques:**
  1. **Manutenção do Grafo**
     - **`adicionar_vertice`:** Adiciona um novo vértice ao grafo, expandindo todas as representações. Custo: \(O(n)\) (adicionar uma linha/coluna nas matrizes).
     - **`adicionar_aresta`/`remover_aresta`:** Atualiza todas as representações do grafo. Custo: Depende da representação mais lenta, geralmente \(O(n)\) para a matriz de incidência.

  2. **Conectividade**
     - **`grafo_conexo`:** Verifica se o grafo é conectado usando busca em profundidade (DFS). Custo: \(O(n + m)\).
     - **`grafo_fortemente_conexo`/`grafo_conexo_fraco`:** Verifica conectividade em grafos direcionados (Kosaraju). Custo: \(O(n + m)\).

  3. **Propriedades de Pontes e Articulações**
     - **`identificar_pontes_naive`:** Remove arestas uma a uma e verifica conectividade. Custo: \(O(m(n + m))\), onde \(n\) são vértices e \(m\) arestas.
     - **`identificar_pontes_tarjan`:** Usa um algoritmo eficiente baseado em DFS para encontrar pontes em \(O(n + m)\).
     - **`identificar_articulacoes`:** Semelhante ao Tarjan, encontra articulações em \(O(n + m)\).

  4. **Eulerianidade**
     - **`grafo_euleriano`:** Verifica se o grafo é euleriano (grau par para todos os vértices). Custo: \(O(n)\).
     - **`fleury`:** Encontra um circuito de Euler, verificando arestas de ponte. Custo: \(O(m^2)\) no pior caso.

---

### **Exportação e Visualização**
- **`exportar_para_gexf`:** Gera um arquivo `.gexf` (usado no Gephi) com a estrutura do grafo.
- **`exportar_para_ppm`:** Cria uma visualização em imagem (formato PPM) do grafo.
- **`exportar_para_txt`:** Gera um arquivo texto com todas as representações do grafo.

---

### **Análise de Custo e Uso**
1. **Grafo Esparso vs Denso**
   - Em grafos **esparsos** (\(m pprox n\)), listas de adjacência são mais eficientes.
   - Em grafos **densos** (\(m pprox n^2\)), matrizes de adjacência são ideais.

2. **Eficiência Algorítmica**
   - Algoritmos baseados em listas de adjacência (\(O(n + m)\)) são melhores em grafos esparsos.
   - Matrizes têm custo fixo \(O(n^2)\), o que pode ser ineficiente para grafos muito grandes.

3. **Tarjan vs Naive**
   - Tarjan é significativamente mais eficiente (\(O(n + m)\)) para detectar pontes/articulações em comparação com o método ingênuo (\(O(m(n + m))\)).

---

### **Conclusão**
O código foi estruturado para ser modular e genérico, permitindo análise detalhada de propriedades de grafos em diferentes representações. Ele prioriza a **versatilidade**, utilizando métodos computacionalmente eficientes sempre que possível.
