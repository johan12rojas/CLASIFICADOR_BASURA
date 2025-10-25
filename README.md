# 🗑️ Clasificador de Residuos con Interfaz Visual

Un clasificador de residuos inteligente que utiliza deep learning para identificar diferentes tipos de basura y mostrar el contenedor de reciclaje correspondiente.

## 📋 Descripción

Este proyecto clasifica residuos en 7 categorías diferentes y muestra visualmente el contenedor de reciclaje apropiado según el sistema de colores estándar:

- **🔵 AZUL** - Papel y Cartón (cardboard, paper)
- **🟢 VERDE** - Vidrio (glass)  
- **🟡 AMARILLO** - Plástico y Metal (plastic, metal)
- **🟤 MARRÓN** - Orgánico (compost, trash)

## 🎯 Características Principales

- ✅ **Interfaz gráfica intuitiva** con widgets interactivos
- ✅ **Clasificación visual** lado a lado (residuo + contenedor)
- ✅ **Optimizado para Windows** con solución a problemas de compatibilidad
- ✅ **Sin duplicación de imágenes** - gestión inteligente de archivos
- ✅ **Resultados organizados** - información clara y legible
- ✅ **Mapeo a 4 contenedores** - sistema de reciclaje estándar

## 🚀 Instalación y Uso

### Requisitos Previos
- Python 3.10 (recomendado)
- Windows 10/11
- VS Code con extensión Jupyter

### Instalación

1. **Clona el repositorio:**
```bash
git clone https://github.com/johan12rojas/CLASIFICADOR_BASURA.git
cd CLASIFICADOR_BASURA
```

2. **Crea un entorno virtual:**
```bash
python -m venv waste_classifier_env
waste_classifier_env\Scripts\activate
```

3. **Instala las dependencias:**
```bash
pip install fastai==2.7.12 opencv-python matplotlib pillow ipywidgets numpy<2
```

4. **Instala Jupyter kernel:**
```bash
python -m ipykernel install --user --name=waste_classifier_env
```

5. **Ejecuta el notebook:**
- Abre `WasteClassifier.ipynb` en VS Code
- Selecciona el kernel `waste_classifier_env`
- Ejecuta las celdas en orden secuencial

## 📁 Estructura del Proyecto

```
CLASIFICADOR_BASURA/
├── WasteClassifier.ipynb          # Notebook principal
├── fotos_para_clasificar/          # Imágenes para clasificar
├── contenedores/                   # Imágenes de contenedores
│   ├── azul.png
│   ├── verde.png
│   ├── amarillo.png
│   └── marron.png
├── fastai-waste-classifier/       # Repositorio original
│   ├── result-resnet50.pkl        # Modelo entrenado
│   └── test-photos/               # Imágenes de prueba
└── README.md
```

## 🔧 Modificaciones Realizadas

### Problemas Resueltos:

1. **❌ Error de compatibilidad Windows:**
   - **Problema:** `NotImplementedError: cannot instantiate 'PosixPath' on your system`
   - **Solución:** Implementé monkey patching para `pathlib.PosixPath` → `WindowsPath`

2. **❌ Conflicto NumPy 1.x vs 2.x:**
   - **Problema:** `A module that was compiled using NumPy 1.x cannot be run in NumPy 2.2.6`
   - **Solución:** Entorno virtual con `numpy<2` y Python 3.10

3. **❌ Interfaz no funcional en Jupyter:**
   - **Problema:** `input()` no funcionaba en VS Code/Jupyter
   - **Solución:** Implementé widgets interactivos con `ipywidgets`

4. **❌ Imágenes duplicadas:**
   - **Problema:** Sistema copiaba imágenes existentes repetidamente
   - **Solución:** Detección inteligente de archivos únicos

5. **❌ Interfaz poco organizada:**
   - **Problema:** Resultados confusos y elementos superpuestos
   - **Solución:** Layout mejorado con separadores visuales y orden lógico

### Mejoras Implementadas:

- 🎨 **Interfaz visual mejorada** con widgets organizados
- 📱 **Dropdown interactivo** para selección de imágenes
- 🖼️ **Visualización lado a lado** (residuo + contenedor)
- 📊 **Resultados claros** con información estructurada
- 🧹 **Gestión automática** de imágenes sin duplicados
- ⚡ **Optimización de rendimiento** con warnings suprimidos

## 📊 Rendimiento del Modelo

- **Precisión:** 98% (según el modelo original)
- **Clases:** 7 categorías de residuos
- **Arquitectura:** ResNet50 con transfer learning
- **Tiempo de inferencia:** <1 segundo por imagen

## 🙏 Créditos y Agradecimientos

### Creadores Originales:
- **[@santit96](https://github.com/santit96)** - Desarrollador principal
- **[@brunomichetti](https://github.com/brunomichetti)** - Colaborador

### Repositorio Original:
- **[fastai-waste-classifier](https://github.com/rootstrap/fastai-waste-classifier)** por Rootstrap

### Google Colab Original:
- **[Colab Notebook](https://colab.research.google.com/drive/1qMxyoVngHiV6E2ePu54o5PiJFr5Ifhku?usp=sharing)** - Versión original en Colab

### Modificaciones por:
- **[@johan12rojas](https://github.com/johan12rojas)** - Adaptación para Windows local y mejoras de interfaz

## 🔄 Diferencias con el Original

| Aspecto | Original | Modificado |
|---------|----------|------------|
| **Plataforma** | Google Colab | Windows Local |
| **Interfaz** | Básica con `input()` | Widgets interactivos |
| **Compatibilidad** | Linux/Mac | Windows optimizado |
| **Gestión de imágenes** | Manual | Automática sin duplicados |
| **Visualización** | Individual | Lado a lado con contenedores |
| **Organización** | Básica | Estructura mejorada |

## 📝 Licencia

Este proyecto está basado en el trabajo original de Rootstrap y los colaboradores mencionados. Las modificaciones están disponibles bajo los mismos términos de licencia del proyecto original.

## 🤝 Contribuciones

Las contribuciones son bienvenidas. Por favor:

1. Fork el proyecto
2. Crea una rama para tu feature (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

## 📞 Contacto

- **GitHub:** [@johan12rojas](https://github.com/johan12rojas)
- **Proyecto:** [CLASIFICADOR_BASURA](https://github.com/johan12rojas/CLASIFICADOR_BASURA)

---

**Nota:** Este proyecto es una adaptación y mejora del clasificador original de Rootstrap, optimizado para funcionar localmente en Windows con una interfaz mejorada.
