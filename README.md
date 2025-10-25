# 🗑️ Clasificador de Residuos con Interfaz Visual

[![Python](https://img.shields.io/badge/Python-3.10-blue.svg)](https://python.org)
[![FastAI](https://img.shields.io/badge/FastAI-2.7.12-green.svg)](https://fast.ai)
[![Windows](https://img.shields.io/badge/Platform-Windows-lightblue.svg)](https://microsoft.com/windows)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

Un clasificador de residuos inteligente que utiliza deep learning para identificar diferentes tipos de basura y mostrar el contenedor de reciclaje correspondiente con una interfaz visual intuitiva.

## 🎯 Demo en Vivo

![Clasificador en Acción](https://img.shields.io/badge/Demo-Available-brightgreen)

**Funcionalidad:** Clasifica automáticamente residuos y muestra el contenedor de reciclaje apropiado según el sistema de colores estándar.

## 📋 Descripción

Este proyecto clasifica residuos en 7 categorías diferentes y muestra visualmente el contenedor de reciclaje apropiado según el sistema de colores estándar:

- **🔵 AZUL** - Papel y Cartón (cardboard, paper)
- **🟢 VERDE** - Vidrio (glass)  
- **🟡 AMARILLO** - Plástico y Metal (plastic, metal)
- **🟤 MARRÓN** - Orgánico (compost, trash)

## ✨ Características Principales

- ✅ **Interfaz gráfica intuitiva** con widgets interactivos
- ✅ **Clasificación visual** lado a lado (residuo + contenedor)
- ✅ **Optimizado para Windows** con solución a problemas de compatibilidad
- ✅ **Sin duplicación de imágenes** - gestión inteligente de archivos
- ✅ **Resultados organizados** - información clara y legible
- ✅ **Mapeo a 4 contenedores** - sistema de reciclaje estándar
- ✅ **98% de precisión** en clasificación de residuos
- ✅ **Tiempo de respuesta** <1 segundo por imagen

## 📸 Capturas de Pantalla

### Interfaz Principal
![Interfaz Principal](https://via.placeholder.com/800x400/4CAF50/FFFFFF?text=Interfaz+Principal+del+Clasificador)

### Resultado de Clasificación
![Resultado](https://via.placeholder.com/800x400/2196F3/FFFFFF?text=Resultado+de+Clasificación+con+Contenedor)

## 🚀 Instalación y Uso

### 📋 Requisitos Previos
- **Python 3.10** (recomendado) - [Descargar](https://python.org/downloads/)
- **Windows 10/11** - Sistema operativo compatible
- **VS Code** con extensión Jupyter - [Descargar](https://code.visualstudio.com/)
- **Git** - Para clonar el repositorio

### ⚡ Instalación Rápida

```bash
# 1. Clona el repositorio
git clone https://github.com/johan12rojas/CLASIFICADOR_BASURA.git
cd CLASIFICADOR_BASURA

# 2. Crea y activa entorno virtual
python -m venv waste_classifier_env
waste_classifier_env\Scripts\activate

# 3. Instala dependencias
pip install fastai==2.7.12 opencv-python matplotlib pillow ipywidgets numpy<2

# 4. Instala kernel de Jupyter
python -m ipykernel install --user --name=waste_classifier_env
```

### 🎯 Uso del Clasificador

1. **Abre VS Code** y navega al proyecto
2. **Abre** `WasteClassifier.ipynb`
3. **Selecciona** el kernel `waste_classifier_env`
4. **Ejecuta** las celdas en orden secuencial (1-10)
5. **Usa** la interfaz gráfica para clasificar imágenes

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

## 🧠 Modelo de Predicción - Funcionamiento Técnico

### **Arquitectura del Modelo:**
- **Base:** ResNet50 (Residual Neural Network con 50 capas)
- **Técnica:** Transfer Learning (aprendizaje por transferencia)
- **Framework:** FastAI 2.7.12
- **Precisión:** 98% en el dataset de validación

### **Proceso de Clasificación:**

#### **1. Preprocesamiento de Imagen:**
```python
# El modelo recibe la imagen y la procesa automáticamente:
# - Redimensionamiento a 224x224 píxeles
# - Normalización de valores RGB (0-255 → 0-1)
# - Aumento de datos (data augmentation) durante entrenamiento
```

#### **2. Inferencia con ResNet50:**
```python
# Flujo de datos a través de la red:
prediction = learn_loaded.predict(image_path)
# Retorna: (clase_predicha, índice_clase, probabilidades_por_clase)
```

#### **3. Estructura de la Predicción:**
- **`prediction[0]`**: Clase predicha (string): `'plastic'`, `'glass'`, etc.
- **`prediction[1]`**: Índice de la clase (tensor): `[2]` para la tercera clase
- **`prediction[2]`**: Probabilidades para todas las clases (array): `[0.1, 0.05, 0.85, ...]`

#### **4. Cálculo de Confianza:**
```python
# Extrae la probabilidad de la clase predicha:
num = prediction[1].numpy().tolist()  # [2]
confidence = prediction[2].numpy()[num]  # 0.85 = 85%
```

### **Mapeo de Clases a Contenedores:**

| Clase Original | Interpretación | Contenedor | Color |
|----------------|----------------|------------|-------|
| `cardboard` | 📦 Cartón | `azul.png` | 🔵 Azul |
| `paper` | 📄 Papel | `azul.png` | 🔵 Azul |
| `glass` | 🍷 Vidrio | `verde.png` | 🟢 Verde |
| `plastic` | 🥤 Plástico | `amarillo.png` | 🟡 Amarillo |
| `metal` | 🔩 Metal | `amarillo.png` | 🟡 Amarillo |
| `compost` | 🌱 Compost/Orgánico | `marron.png` | 🟤 Marrón |
| `trash` | 🗑️ Basura General | `marron.png` | 🟤 Marrón |

### **Algoritmo de Decisión:**
```python
# 1. El modelo analiza la imagen pixel por pixel
# 2. Extrae características visuales (formas, colores, texturas)
# 3. Compara con patrones aprendidos durante el entrenamiento
# 4. Asigna probabilidades a cada una de las 7 clases
# 5. Selecciona la clase con mayor probabilidad
# 6. Mapea la clase a su contenedor de reciclaje correspondiente
```

### **Características Técnicas del Modelo:**

#### **Entrenamiento Original:**
- **Dataset:** Imágenes descargadas via Bing Search API
- **División:** Train/Test automática
- **Técnica:** Fine-tuning de ResNet50 pre-entrenado en ImageNet
- **Optimizador:** Adam con learning rate adaptativo
- **Épocas:** Entrenado hasta convergencia (~20-30 épocas)

#### **Transfer Learning:**
```python
# El modelo aprovecha conocimiento previo:
# 1. ResNet50 ya sabe reconocer formas básicas (ImageNet)
# 2. Se adapta específicamente a residuos (fine-tuning)
# 3. Últimas capas se reentrenan para las 7 clases específicas
```

#### **Precisión y Validación:**
- **Accuracy:** 98% en conjunto de validación
- **Matriz de confusión:** Disponible en `classification_matrix_resnet50.png`
- **Clases más precisas:** Glass, Metal, Plastic (>95%)
- **Clases más desafiantes:** Compost, Trash (90-95%)

### **Optimizaciones Implementadas:**

#### **Para Windows:**
```python
# Solución al error PosixPath:
class WindowsUnpickler(pickle.Unpickler):
    def find_class(self, module, name):
        if module == 'pathlib' and name == 'PosixPath':
            return WindowsPath  # Convierte PosixPath → WindowsPath
        return super().find_class(module, name)
```

#### **Para Rendimiento:**
- **Supresión de warnings:** `warnings.filterwarnings('ignore')`
- **Configuración matplotlib:** Colores de fondo optimizados
- **Gestión de memoria:** Carga eficiente de imágenes con PIL

### **Limitaciones del Modelo:**
- **Resolución:** Optimizado para imágenes ~224x224 píxeles
- **Formato:** Funciona mejor con imágenes claras y bien iluminadas
- **Objetos mixtos:** Puede confundirse con residuos que contienen múltiples materiales
- **Nuevos materiales:** No reconoce materiales no vistos durante entrenamiento

## 📊 Rendimiento del Modelo

- **Precisión:** 98% (según el modelo original)
- **Clases:** 7 categorías de residuos
- **Arquitectura:** ResNet50 con transfer learning
- **Tiempo de inferencia:** <1 segundo por imagen
- **Tamaño del modelo:** ~100MB (result-resnet50.pkl)

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

## 🔧 Troubleshooting

### Problemas Comunes y Soluciones

#### ❌ Error: `NotImplementedError: cannot instantiate 'PosixPath'`
**Solución:** El código ya incluye el fix automático. Si persiste:
```bash
# Reinstala las dependencias
pip uninstall fastai
pip install fastai==2.7.12
```

#### ❌ Error: `A module that was compiled using NumPy 1.x`
**Solución:** Usa el entorno virtual con NumPy <2:
```bash
pip install numpy<2
```

#### ❌ Error: `ModuleNotFoundError: No module named 'ipywidgets'`
**Solución:** Instala ipywidgets:
```bash
pip install ipywidgets
jupyter nbextension enable --py widgetsnbextension
```

#### ❌ Las imágenes no se muestran
**Solución:** Verifica que las carpetas existan:
```bash
# Verifica estructura
ls fotos_para_clasificar/
ls contenedores/
```

## 🤝 Contribuciones

¡Las contribuciones son bienvenidas! Este proyecto está abierto a mejoras y nuevas funcionalidades.

### 🚀 Cómo Contribuir

1. **Fork** el proyecto
2. **Crea** una rama para tu feature (`git checkout -b feature/AmazingFeature`)
3. **Commit** tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. **Push** a la rama (`git push origin feature/AmazingFeature`)
5. **Abre** un Pull Request

### 💡 Ideas para Contribuir

- 🌍 **Soporte multiidioma** - Traducir la interfaz
- 📱 **App móvil** - Versión para Android/iOS
- 🔄 **API REST** - Servicio web para integración
- 📊 **Dashboard** - Estadísticas de clasificación
- 🎨 **Temas visuales** - Diferentes estilos de interfaz
- 🧪 **Tests automatizados** - Suite de pruebas
- 📖 **Documentación** - Guías adicionales

## 🗺️ Roadmap

### Próximas Características

- [ ] 🌍 **Soporte multiidioma** (Inglés, Francés, Alemán)
- [ ] 📱 **Aplicación móvil** para Android/iOS
- [ ] 🔄 **API REST** para integración con otros sistemas
- [ ] 📊 **Dashboard web** con estadísticas en tiempo real
- [ ] 🎨 **Temas personalizables** para la interfaz
- [ ] 🧪 **Suite de tests** automatizados
- [ ] 📖 **Documentación interactiva** con ejemplos
- [ ] 🔍 **Clasificación de objetos mixtos** mejorada
- [ ] 📈 **Métricas de rendimiento** en tiempo real
- [ ] 🎯 **Modo batch** para procesar múltiples imágenes

### Versiones Futuras

- **v2.0** - API REST y dashboard web
- **v2.1** - Aplicación móvil
- **v3.0** - Soporte multiidioma y temas
- **v3.1** - Clasificación de objetos mixtos

## 📞 Contacto y Soporte

### 👨‍💻 Desarrollador
- **GitHub:** [@johan12rojas](https://github.com/johan12rojas)
- **Proyecto:** [CLASIFICADOR_BASURA](https://github.com/johan12rojas/CLASIFICADOR_BASURA)

### 🆘 Soporte
- **Issues:** [Reportar problemas](https://github.com/johan12rojas/CLASIFICADOR_BASURA/issues)
- **Discussions:** [Discusiones generales](https://github.com/johan12rojas/CLASIFICADOR_BASURA/discussions)
- **Wiki:** [Documentación adicional](https://github.com/johan12rojas/CLASIFICADOR_BASURA/wiki)

### 📧 Contacto Directo
Para consultas específicas o colaboraciones, puedes contactarme a través de GitHub.

## 📊 Estadísticas del Proyecto

![GitHub stars](https://img.shields.io/github/stars/johan12rojas/CLASIFICADOR_BASURA?style=social)
![GitHub forks](https://img.shields.io/github/forks/johan12rojas/CLASIFICADOR_BASURA?style=social)
![GitHub issues](https://img.shields.io/github/issues/johan12rojas/CLASIFICADOR_BASURA)
![GitHub last commit](https://img.shields.io/github/last-commit/johan12rojas/CLASIFICADOR_BASURA)

---

## 📝 Nota Importante

Este proyecto es una **adaptación y mejora** del clasificador original de Rootstrap, optimizado para funcionar localmente en Windows con una interfaz mejorada. Se mantiene el reconocimiento a los creadores originales y se documentan todas las modificaciones realizadas.

**⭐ Si te gusta este proyecto, ¡dale una estrella en GitHub!**
