## Taller 03 Problemas de Satisfacción de Restricciones 
**Problema:** dado un grafo no dirigido representado por una matriz de adyacencias
simétrica $N \times N$ ($N < 21$, con $1$ = arista existente y $0$ = arista inexistente),
encontrar una asignación de colores a los nodos tal que **dos nodos adyacentes nunca
tengan el mismo color**, usando el **menor número de colores posible**.}

Este problema se modela como un **Problema de Satisfacción de Restricciones (CSP)**:

- **Variables:** los nodos del grafo ($v_0, v_1, \dots, v_{n-1}$).
- **Dominios:** el conjunto de colores disponibles $\{0, 1, \dots, k-1\}$ para cada nodo.
- **Restricciones:** para toda arista $(u, v)$, se debe cumplir $color(u) \neq color(v)$.

Para resolverlo se implementa el algoritmo **BT-FC-DO**:

| Sigla | Significa | Qué hace |
|---|---|---|
| **BT** | *Backtracking* | Búsqueda en profundidad que asigna un color a un nodo y retrocede (backtrack) si una elección lleva a un callejón sin salida. |
| **FC** | *Forward Checking* | Cada vez que se asigna un color a un nodo, se elimina ese color de los dominios de sus vecinos aún no asignados. Si el dominio de algún vecino queda vacío, se detecta el fallo **antes** de seguir bajando en el árbol de búsqueda (poda temprana). |
| **DO** | *Dynamic Ordering* | En cada paso se elige el **siguiente nodo a colorear dinámicamente**, usando la heurística MRV (*Minimum Remaining Values*: el nodo con menos colores disponibles en su dominio) y, como criterio de desempate, el nodo de **mayor grado** (más conexiones), ya que suele ser el más restrictivo. |

Estructura del cuaderno:
1. Utilidades y validación.
2. Carga del grafo (desde archivo `.txt` o generado aleatoriamente).
3. Algoritmo BT-FC-DO.
4. Visualización del grafo coloreado.
5. Celda de ejecución donde se elige el origen del grafo y se corre todo el proceso.

### Ejemplo de Prueba: Grafo de Prueba ($N=5$)

Como caso de pruebas se utiliza un **Grafo No Dirigido de 5 Vértices**, el cual permite verificar la propagación de colores y la poda del algoritmo BT-FC-DO en tiempo real.

* **Representación en archivo plano (`grafo.txt`):**
  ```text
  0 1 0 1 1
  1 0 1 0 1
  0 1 0 1 1
  1 0 1 0 1
  1 1 1 1 0
**Resultado**:
- Número mínimo de colores usados (número cromático): 3
- Asignación por nodo: {5: 1, 1: 2, 2: 3, 3: 2, 4: 3}
<img width="514" height="590" alt="image" src="https://github.com/user-attachments/assets/7c5528c3-aedf-46ad-9cd9-d6bf014ed7b9" />
