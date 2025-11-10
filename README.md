# Formulario de Matemáticas - Integradora

Proyecto LaTeX organizado de forma modular para el reporte de matemáticas integradora.

## 📁 Estructura del Proyecto

```
formulario-latex/
│
├── main.tex                    # Archivo principal (compilar este)
├── reporte_original.tex        # Backup del archivo original
├── reporte.pdf                 # PDF del archivo original
├── main.pdf                    # PDF generado con la nueva estructura
│
├── config/                     # Configuración del documento
│   └── preambulo.tex          # Paquetes, colores y estilos personalizados
│
├── portada/                    # Portada del documento
│   └── portada.tex            # Título, autores e imagen de portada
│
├── unidades/                   # Unidades de aprendizaje
│   ├── unidad1.tex            # Unidad I: Funciones de varias variables (completa)
│   ├── unidad2.tex            # Unidad II: Derivadas Parciales (pendiente)
│   ├── unidad3.tex            # Unidad III: Integral múltiple (pendiente)
│   └── unidad4.tex            # Unidad IV: Funciones vectoriales (pendiente)
│
├── imagenes/                   # Recursos gráficos
│   └── mate.jpg               # Imagen de portada
│
└── referencias/                # Bibliografía
    └── referencias.tex        # Referencias en formato APA
```

## 🚀 Compilación

Para compilar el documento, ejecuta:

```bash
pdflatex main.tex
pdflatex main.tex  # Segunda vez para actualizar el índice
```

O simplemente compila `main.tex` desde tu editor LaTeX favorito (TeXstudio, Overleaf, etc.).

## 📝 Contenido de las Unidades

### Unidad I: Funciones de varias variables
- **Funciones de varias variables**
  - Funciones escalares de varias variables
  - Dominio y rango
  - Funciones explícitas e implícitas
  - Aplicaciones prácticas
- **Planos y superficies**
  - Curvas de nivel
  - Superficies cuadráticas (elipsoides, cono, paraboloides, hiperboloides)
  - Graficación con TikZ/PGFPlots
- **Límites y continuidad en funciones de 3 variables**
  - Definición y conceptos
  - Racionalización de límites
  - Ejercicios prácticos resueltos
  - Visualización gráfica

### Unidad II: Derivadas Parciales
- **La derivada parcial**
  - Construcción geométrica (pendiente)
  - Reglas de derivación parcial (pendiente)
  - Regla de la cadena para varias variables (pendiente)
- **Vector gradiente y derivada direccional**
  - Cálculo e interpretación geométrica (pendiente)
  - Representación de vectores gradientes en superficies (pendiente)
- **Extremos de funciones multivariables**
  - Valores críticos (pendiente)
  - Máximos y mínimos (pendiente)
  - Método de multiplicadores de Lagrange (pendiente)
  - Representación gráfica (pendiente)

### Unidad III: Integral múltiple (Pendiente)
- Integrales dobles
- Integrales triples
- Cambio de variable en integrales múltiples
- Aplicaciones de integrales múltiples

### Unidad IV: Funciones vectoriales (Pendiente)
- Funciones vectoriales de una variable
- Derivadas e integrales de funciones vectoriales
- Longitud de arco y curvatura
- Aplicaciones de funciones vectoriales

## ✏️ Cómo Editar

### Para añadir contenido a una unidad:
1. Abre el archivo correspondiente en `unidades/`
2. Edita el contenido
3. Guarda y compila `main.tex`

### Para añadir una nueva unidad:
1. Crea un nuevo archivo `unidades/unidadX.tex`
2. Añade la línea en `main.tex`:
   ```latex
   \input{unidades/unidadX}
   \newpage
   ```

### Para añadir imágenes:
1. Guarda la imagen en la carpeta `imagenes/`
2. Usa en cualquier archivo `.tex`:
   ```latex
   \includegraphics[width=0.6\textwidth]{imagenes/nombre_imagen.jpg}
   ```

## 🎨 Estilos Personalizados

El documento incluye cajas personalizadas definidas en `config/preambulo.tex`:

- `\begin{TemaBox}[Título]...\end{TemaBox}` - Caja para temas principales
- `\begin{InfoBox}...\end{InfoBox}` - Caja informativa
- `\begin{EjercicioBox}[Título]...\end{EjercicioBox}` - Caja para ejercicios

## 🏫 Información del Proyecto

**Universidad:** Universidad Tecnológica Emiliano Zapata del Estado de Morelos  
**División:** División Académica de Tecnologías de la Información y Diseño  
**Carrera:** Ingeniería en Desarrollo y Gestión de Software  
**Materia:** Matemáticas para Ingeniería I  
**Profesor:** M.C. Jorge Yusef Colin Castillo  
**Grupo:** 7°C  

## 👥 Integrantes del Equipo

- Hernández Sánchez Katia Alexandra
- Higareda Vázquez María del Pilar
- León Flores Axel Daniel
- Miranda Roldán Jose Luis

## 📚 Referencias

Todas las referencias bibliográficas están organizadas en `referencias/referencias.tex` en formato APA.

---

**Nota:** Este proyecto utiliza paquetes como `tcolorbox`, `tikz`, `pgfplots` para gráficas y visualizaciones matemáticas avanzadas.

