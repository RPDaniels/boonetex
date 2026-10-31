# Boonetex · Boolean Network Explorer

**[English](#english) · [Español](#español)**

| Language | Open the app |
|---|---|
| English | [Boolean Network Explorer.html](https://github.com/RPDaniels/boonetex/blob/main/Boolean%20Network%20Explorer.html) |
| Español | [Explorador de Redes Booleanas.html](https://github.com/RPDaniels/boonetex/blob/main/Explorador%20de%20Redes%20Booleanas.html) |

---

## English

An interactive, single-file web app for exploring the dynamics of small Boolean networks. You define a network as an N×N connection matrix **W**. Each of the 2ᴺ possible states of the network is then mapped to its successor, and the app draws the whole state space as a **basin of attraction field**. In that drawing you can see the attractors (fixed points and cycles), the basins that drain into each one, and the transient trees that lead to them.

### The idea

The network has N nodes, x₁ … x_N, and each node is either 0 or 1. The state of the network is a binary vector **x** ∈ {0,1}ᴺ. Multiplying the matrix by the state vector gives the next state:

```
x(t+1) = W ⊙ x(t)
```

There are only 2ᴺ states, so every trajectory must eventually repeat. That means every state ends up in an **attractor**: either a fixed point or a cycle. The set of states that ends up in the same attractor is its **basin of attraction**. With 5 nodes there are 32 states. With 10 nodes there are 1024.

### Update rules

The "multiplication" `W ⊙ x` can be interpreted in three ways:

| Rule | Definition | Matrix values |
|---|---|---|
| **Boolean** | xᵢ′ = OR_j (Wᵢⱼ AND xⱼ). A node turns on if any of its inputs is active. | 0, 1 |
| **XOR (mod 2)** | xᵢ′ = Σⱼ Wᵢⱼ·xⱼ mod 2. A linear network over GF(2): each node becomes the parity of its inputs. | 0, 1 |
| **Threshold ±** | hᵢ = Σⱼ Wᵢⱼ·xⱼ. Then xᵢ′ = 1 if hᵢ > 0, xᵢ′ = 0 if hᵢ < 0, and xᵢ keeps its value if hᵢ = 0. | −1, 0, 1 (red = inhibition) |

In the matrix, row *i* holds the inputs that node xᵢ receives, and column *j* holds the influence of node xⱼ.

### Features

- **Editable matrix from 3×3 to 10×10** (8 to 1024 states). Tap a cell to toggle its value. In threshold mode a cell cycles through 0 → 1 → −1.
- **Built-in examples** that adapt to every size:
  - Mixed
  - Shift ring
  - Identity
  - Rule 90 on a ring
  - Maximal-length shift register: a single cycle that visits 2ᴺ−1 states
  - Activation–inhibition
- **Random** matrix generator.
- **Basin of attraction field.** The attractor sits at the centre of each basin and the transient trees radiate outwards. The drawing marks:
  - **Garden of Eden** states (states with no predecessor) as hollow nodes
  - attractor states as ringed nodes
  - each basin in its own colour

  You can switch the state labels on and off, and choose between fitting the whole field to the screen width or showing it at full scale with horizontal scrolling.
- **Trajectories.** Tap any state to highlight its path to the attractor. **Step** advances one time step, and **Run** animates the dynamics on the wiring diagram as the nodes switch on and off.
- **Summary figures:** the number of attractors, fixed points and limit cycles, the maximum period, the number of Garden of Eden states and the longest transient.
- **Attractor list** showing each attractor's cycle and basin size. Tap an attractor to highlight its basin.
- **Full transition table** listing every state and its successor.
- **Configurations.** You can save a configuration under a name, then load it again or delete it later. You can also:
  - copy the configuration as a JSON code
  - paste a code to load it
  - open a `.json` file

### Configuration format

```json
{
  "format": "boolean-network",
  "v": 1,
  "name": "Period-6 cycle",
  "n": 5,
  "rule": "umb",
  "W": [[0,-1,0,1,0],[1,0,-1,0,0],[0,1,0,0,-1],[-1,0,1,0,0],[0,0,0,1,-1]]
}
```

`rule` is one of `bool`, `mod2` or `umb` (threshold). The Spanish version writes its codes with Spanish field names (`formato`, `nombre`, `regla`). Both versions read both formats, so a configuration saved in one language can be loaded in the other.

### Running it

The app is a single self-contained HTML file. All CSS and JavaScript are inline, and the only external resource is Google Fonts. To run it, download the file and open it in any modern browser. No build step, server or installation is needed.

Saved configurations are kept in the browser's local storage. To move a configuration to another browser or device, use **Copy code** or a `.json` file.

---

## Español

Una aplicación web interactiva, contenida en un único archivo, para explorar la dinámica de redes booleanas pequeñas. Defines la red con una matriz de conexiones **W** de N×N. La aplicación calcula a qué estado lleva cada uno de los 2ᴺ estados posibles y dibuja el espacio de estados completo como un **campo de cuencas de atracción**. En ese dibujo se ven los atractores (puntos fijos y ciclos), las cuencas que desembocan en cada uno y los árboles transitorios que llevan hasta ellos.

### La idea

La red tiene N nodos, x₁ … x_N, y cada nodo vale 0 o 1. El estado de la red es un vector binario **x** ∈ {0,1}ᴺ. Al multiplicar la matriz por el vector de estado se obtiene el estado siguiente:

```
x(t+1) = W ⊙ x(t)
```

Como solo hay 2ᴺ estados, toda trayectoria acaba repitiéndose. Eso significa que todo estado termina en un **atractor**: un punto fijo o un ciclo. El conjunto de estados que acaba en el mismo atractor es su **cuenca de atracción**. Con 5 nodos hay 32 estados; con 10 nodos hay 1024.

### Reglas de actualización

La "multiplicación" `W ⊙ x` puede interpretarse de tres formas:

| Regla | Definición | Valores de la matriz |
|---|---|---|
| **Booleana** | xᵢ′ = OR_j (Wᵢⱼ AND xⱼ). Un nodo se enciende si alguna de sus entradas está activa. | 0, 1 |
| **XOR (mod 2)** | xᵢ′ = Σⱼ Wᵢⱼ·xⱼ mod 2. Una red lineal sobre GF(2): cada nodo pasa a ser la paridad de sus entradas. | 0, 1 |
| **Umbral ±** | hᵢ = Σⱼ Wᵢⱼ·xⱼ. Después, xᵢ′ = 1 si hᵢ > 0, xᵢ′ = 0 si hᵢ < 0, y xᵢ conserva su valor si hᵢ = 0. | −1, 0, 1 (rojo = inhibición) |

En la matriz, la fila *i* contiene las entradas que recibe el nodo xᵢ, y la columna *j* contiene la influencia del nodo xⱼ.

### Funciones

- **Matriz editable de 3×3 a 10×10** (de 8 a 1024 estados). Toca una celda para cambiar su valor. En modo umbral, cada celda va pasando por 0 → 1 → −1.
- **Ejemplos incluidos** que se adaptan a cada tamaño:
  - Mixta
  - Anillo de desplazamiento
  - Identidad
  - Regla 90 en anillo
  - Registro de ciclo máximo: un único ciclo que recorre 2ᴺ−1 estados
  - Activación-inhibición
- **Generador de matrices aleatorias.**
- **Campo de cuencas de atracción.** El atractor ocupa el centro de cada cuenca y los árboles transitorios salen hacia fuera. El dibujo marca:
  - los estados **Jardín del Edén** (estados sin predecesor) como nodos huecos
  - los estados del atractor con un anillo
  - cada cuenca con su propio color

  Puedes activar o desactivar las etiquetas de los estados, y elegir entre ajustar todo el campo al ancho de la pantalla o verlo a tamaño real con desplazamiento horizontal.
- **Trayectorias.** Toca cualquier estado para resaltar su camino hasta el atractor. **Paso** avanza un instante de tiempo y **Ejecutar** anima la dinámica sobre el diagrama de la red, encendiendo y apagando los nodos.
- **Cifras resumen:** el número de atractores, de puntos fijos y de ciclos límite, el periodo máximo, el número de estados Jardín del Edén y el transitorio más largo.
- **Lista de atractores** con el ciclo de cada atractor y el tamaño de su cuenca. Toca un atractor para resaltar su cuenca.
- **Tabla de transiciones completa** con cada estado y su sucesor.
- **Configuraciones.** Puedes guardar una configuración con un nombre y después cargarla o borrarla. También puedes:
  - copiar la configuración como código JSON
  - pegar un código para cargarlo
  - abrir un archivo `.json`

### Formato de configuración

```json
{
  "formato": "red-booleana",
  "v": 1,
  "nombre": "Ciclo de periodo 6",
  "n": 5,
  "regla": "umb",
  "W": [[0,-1,0,1,0],[1,0,-1,0,0],[0,1,0,0,-1],[-1,0,1,0,0],[0,0,0,1,-1]]
}
```

`regla` puede ser `bool`, `mod2` o `umb` (umbral). La versión inglesa escribe sus códigos con nombres de campo en inglés (`format`, `name`, `rule`). Las dos versiones leen ambos formatos, así que una configuración guardada en un idioma se puede cargar en el otro.

### Cómo usarla

La aplicación es un único archivo HTML autocontenido. Todo el CSS y el JavaScript van dentro del archivo, y el único recurso externo son las fuentes de Google Fonts. Para usarla, descarga el archivo y ábrelo en cualquier navegador moderno. No hace falta compilar, ni un servidor, ni instalar nada.

Las configuraciones guardadas se conservan en el almacenamiento local del navegador. Para llevar una configuración a otro navegador o dispositivo, usa **Copiar código** o un archivo `.json`.
