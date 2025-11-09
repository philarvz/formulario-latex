# 📋 Instrucciones de Configuración - Proyecto LaTeX

## 🎯 Objetivo
Este documento te guiará paso a paso para configurar un entorno completo de LaTeX en Windows, permitiéndote compilar archivos `.tex` a PDF y visualizarlos automáticamente.

---

## 🖥️ Requisitos Previos

- **Sistema Operativo:** Windows 10/11
- **GitHub Copilot** o **Claude Sonnet 4.5** (como asistente de IA)
- **VS Code** (recomendado como editor)|
- **Conexión a Internet** (para descarga de paquetes)

---

## 📦 Paso 1: Instalación de MiKTeX

MiKTeX es la distribución de LaTeX más completa para Windows. Incluye todos los paquetes necesarios para compilar documentos LaTeX profesionales.

### Opción A: Instalación con winget (Recomendado)

1. Abre una **terminal bash** en VS Code (Ctrl + `)

2. Ejecuta el siguiente comando:
```bash
winget install MiKTeX.MiKTeX --accept-package-agreements --accept-source-agreements
```

3. Espera de 5-10 minutos mientras se descarga e instala (~138 MB)

4. **Importante:** Cierra y vuelve a abrir la terminal para que se actualice el PATH

### Opción B: Instalación manual

1. Ve a [https://miktex.org/download](https://miktex.org/download)
2. Descarga el instalador de **Basic MiKTeX** para Windows (x64)
3. Ejecuta el instalador y sigue las instrucciones
4. Selecciona "Install missing packages on-the-fly: Yes"

### Verificación de la instalación

```bash
# Verifica que pdflatex esté disponible
pdflatex --version
```

Si ves la versión de pdfTeX, ¡la instalación fue exitosa! ✅

---

## 🔧 Paso 2: Configuración de Rutas

### Ubicación de pdflatex en Windows

Por defecto, MiKTeX se instala en:
```
C:\Users\[TU_USUARIO]\AppData\Local\Programs\MiKTeX\miktex\bin\x64\
```

O también puede estar en:
```
C:\Program Files\MiKTeX\miktex\bin\x64\
```

### Verificar la ruta exacta

```bash
# En bash de VS Code
where pdflatex

# O buscar manualmente
ls "$USERPROFILE/AppData/Local/Programs/MiKTeX/miktex/bin/x64/" | grep pdflatex
```

---

## 📝 Paso 3: Estructura del Proyecto

Asegúrate de tener la siguiente estructura en tu carpeta:

```
reporte-matematicas/
├── reporte.tex              # Archivo LaTeX principal
├── mate.jpg                 # Imagen de portada (opcional)
├── README.md                # Documentación del proyecto
└── SETUP-INSTRUCTIONS.md    # Este archivo
```

---

## 🚀 Paso 4: Compilación de Documentos LaTeX

### Método 1: Compilación básica (una pasada)

```bash
cd "ruta/a/tu/proyecto/reporte-matematicas"

pdflatex -interaction=nonstopmode reporte.tex
```

### Método 2: Compilación completa (dos pasadas para índices)

```bash
# Primera compilación (genera archivos auxiliares)
pdflatex -interaction=nonstopmode reporte.tex

# Segunda compilación (actualiza índice y referencias)
pdflatex -interaction=nonstopmode reporte.tex
```

### Método 3: Compilación con ruta completa (si pdflatex no está en PATH)

```bash
"$USERPROFILE/AppData/Local/Programs/MiKTeX/miktex/bin/x64/pdflatex.exe" -interaction=nonstopmode reporte.tex
```

---

## 🎨 Paso 5: Visualización del PDF

### Abrir automáticamente el PDF generado

```bash
# En Windows (bash)
start reporte.pdf

# O con ruta completa
start "C:/ruta/completa/reporte-matematicas/reporte.pdf"
```

### Editores de PDF recomendados

- **Adobe Acrobat Reader** (más común)
- **Microsoft Edge** (viene preinstalado)
- **SumatraPDF** (ligero y rápido)
- **Foxit Reader**

---

## 🔄 Paso 6: Script de Compilación Automática

Crea un script para automatizar todo el proceso:

### Archivo: `compile.sh`

```bash
#!/bin/bash

# Script de compilación automática de LaTeX
PROJECT_DIR="c:\Users\ADMIN\OneDrive\Escritorio\latez\reporte-matematicas"
PDFLATEX="$USERPROFILE/AppData/Local/Programs/MiKTeX/miktex/bin/x64/pdflatex.exe"

echo "🔨 Compilando documento LaTeX..."
cd "$PROJECT_DIR"

# Limpiar archivos antiguos
rm -f reporte.pdf reporte.aux reporte.log reporte.out reporte.toc

# Primera compilación
echo "📝 Primera pasada..."
"$PDFLATEX" -interaction=nonstopmode reporte.tex > /dev/null 2>&1

if [ $? -eq 0 ]; then
    echo "✅ Primera compilación exitosa"
    
    # Segunda compilación (para índices)
    echo "📝 Segunda pasada..."
    "$PDFLATEX" -interaction=nonstopmode reporte.tex > /dev/null 2>&1
    
    if [ $? -eq 0 ]; then
        echo "✅ Compilación completa exitosa"
        echo "📄 PDF generado: reporte.pdf"
        
        # Abrir el PDF
        start reporte.pdf
        echo "👁️ PDF abierto para visualización"
    else
        echo "❌ Error en segunda compilación"
        echo "📋 Revisa el archivo reporte.log para detalles"
    fi
else
    echo "❌ Error en primera compilación"
    echo "📋 Revisa el archivo reporte.log para detalles"
fi
```

### Uso del script

```bash
# Dar permisos de ejecución
chmod +x compile.sh

# Ejecutar
./compile.sh
```

---

## 🛠️ Paso 7: Solución de Problemas Comunes

### Problema 1: "bash: pdflatex: command not found"

**Solución:**
```bash
# Opción 1: Usar ruta completa
"$USERPROFILE/AppData/Local/Programs/MiKTeX/miktex/bin/x64/pdflatex.exe" reporte.tex

# Opción 2: Agregar al PATH temporalmente
export PATH="$PATH:$USERPROFILE/AppData/Local/Programs/MiKTeX/miktex/bin/x64"
pdflatex reporte.tex
```

### Problema 2: "cannot remove 'reporte.pdf': Device or resource busy"

**Causa:** El PDF está abierto en un visor.

**Solución:**
```bash
# Cerrar el visor automáticamente
taskkill //F //IM Acrobat.exe 2>/dev/null
taskkill //F //IM AcroRd32.exe 2>/dev/null

# Esperar 2 segundos
sleep 2

# Compilar nuevamente
pdflatex -interaction=nonstopmode reporte.tex
```

### Problema 3: Faltan paquetes LaTeX

**Error típico:** `! LaTeX Error: File 'tcolorbox.sty' not found.`

**Solución:**
```bash
# MiKTeX debería instalar paquetes automáticamente
# Si no lo hace, instálalo manualmente:

# Abrir MiKTeX Console
miktex-console

# O desde terminal
mpm --install=tcolorbox
mpm --install=pgfplots
mpm --install=tikzfill
```

### Problema 4: Errores de compilación en el código LaTeX

**Solución:**
```bash
# Ver errores detallados (sin -interaction=nonstopmode)
pdflatex reporte.tex

# O revisar el log
cat reporte.log | grep "Error"
cat reporte.log | grep "Warning"
```

---

## 📚 Paso 8: Paquetes LaTeX Utilizados en Este Proyecto

El documento `reporte.tex` utiliza los siguientes paquetes:

```latex
\usepackage[utf8]{inputenc}          % Codificación UTF-8
\usepackage[T1]{fontenc}              % Codificación de fuentes
\usepackage[spanish]{babel}           % Idioma español
\usepackage{graphicx}                 % Imágenes
\usepackage{amsmath, amssymb}         % Símbolos matemáticos
\usepackage[dvipsnames]{xcolor}       % Colores extendidos
\usepackage{geometry}                 % Márgenes
\usepackage{hyperref}                 % Hipervínculos
\usepackage[skins,breakable]{tcolorbox}  % Cajas de colores
\usepackage{tikz}                     % Gráficos vectoriales
\usepackage{pgfplots}                 % Gráficos matemáticos
```

MiKTeX instalará estos paquetes automáticamente la primera vez que compiles.

---

## 🤖 Paso 9: Uso con GitHub Copilot / Claude Sonnet

### Comandos útiles para dar al asistente de IA

1. **Compilar el documento:**
```
"Compila el archivo reporte.tex ubicado en [RUTA] usando pdflatex"
```

2. **Compilar y abrir:**
```
"Compila reporte.tex dos veces para actualizar el índice y luego abre el PDF"
```

3. **Limpiar y recompilar:**
```
"Elimina los archivos auxiliares (.aux, .log, .out, .toc) y recompila reporte.tex"
```

4. **Solucionar errores:**
```
"Hay un error de compilación en reporte.tex, revisa el archivo reporte.log y sugiere soluciones"
```

### Prompt completo para el asistente:

```
Necesito compilar un documento LaTeX en Windows. El archivo es reporte.tex ubicado en 
[TU_RUTA]. Usa pdflatex que está en "$USERPROFILE/AppData/Local/Programs/MiKTeX/miktex/bin/x64/". 
Compila dos veces para actualizar el índice y luego abre el PDF automáticamente con 'start reporte.pdf'.
```

---

## 📊 Paso 10: Comandos de Referencia Rápida

### Compilación

```bash
# Compilación básica
pdflatex reporte.tex

# Con modo no interactivo
pdflatex -interaction=nonstopmode reporte.tex

# Redirigir salida
pdflatex -interaction=nonstopmode reporte.tex > /dev/null 2>&1

# Compilación completa (dos veces)
pdflatex -interaction=nonstopmode reporte.tex && pdflatex -interaction=nonstopmode reporte.tex
```

### Limpieza

```bash
# Eliminar archivos auxiliares
rm -f *.aux *.log *.out *.toc *.lof *.lot *.fls *.fdb_latexmk *.synctex.gz

# Eliminar todo excepto .tex y PDF
rm -f !(*.tex|*.pdf|*.jpg|*.png)
```

### Visualización

```bash
# Abrir PDF
start reporte.pdf

# Abrir con aplicación específica
start "C:\Program Files\Adobe\Acrobat DC\Acrobat\Acrobat.exe" reporte.pdf
```

---

## ✅ Verificación Final

Ejecuta este checklist para confirmar que todo funciona:

- [ ] MiKTeX está instalado (`pdflatex --version` funciona)
- [ ] El archivo `reporte.tex` existe en tu carpeta
- [ ] Puedes compilar sin errores (`pdflatex reporte.tex`)
- [ ] Se genera el archivo `reporte.pdf`
- [ ] Puedes abrir el PDF automáticamente (`start reporte.pdf`)
- [ ] La segunda compilación actualiza el índice correctamente

---

## 📞 Recursos Adicionales

- **Documentación oficial de MiKTeX:** [https://docs.miktex.org/](https://docs.miktex.org/)
- **LaTeX Project:** [https://www.latex-project.org/](https://www.latex-project.org/)
- **Overleaf Learn:** [https://www.overleaf.com/learn](https://www.overleaf.com/learn)
- **CTAN (Paquetes LaTeX):** [https://ctan.org/](https://ctan.org/)
- **Stack Exchange (TeX):** [https://tex.stackexchange.com/](https://tex.stackexchange.com/)

---

## 🎓 Notas Finales

Este entorno está completamente configurado para trabajar con documentos LaTeX profesionales que incluyen:

- ✅ Matemáticas avanzadas (ecuaciones, matrices, límites)
- ✅ Gráficos vectoriales (TikZ/PGFPlots)
- ✅ Cajas de colores personalizadas (tcolorbox)
- ✅ Índices y referencias automáticas
- ✅ Hipervínculos internos y externos
- ✅ Formato APA para bibliografía

**¡Listo para crear documentos académicos de alta calidad!** 🎉

---

*Última actualización: 26 de octubre de 2025*
*Creado por: GitHub Copilot / Claude Sonnet 4.5*
