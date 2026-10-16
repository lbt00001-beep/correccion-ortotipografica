> **Repositorio principal:** `lbt00001-beep/correccion-ortotipografica`. Consolidación de las dos copias y entrega 2.2.1: [MANTENIMIENTO.md](MANTENIMIENTO.md).

# App de Corrección Ortotipográfica

Sistema profesional de corrección ortotipográfica y de estilo para documentos Word (.docx) en español. Dos modos de operación: básico y profesional.

## 🚀 Características

### ✅ Fase 1: Versión Básica
Correcciones directas (sin Track Changes):
- **LanguageTool**: Corrección gramatical automática
- **Reglas RAE**: Ortotipografía (comillas, rayas, espacios duros)
- Procesamiento rápido para documentos finales

### ✅ Fase 2: Versión Profesional
Track Changes (revisiones para aceptar/rechazar):
- **XML OpenXML**: Manipulación directa con `lxml`
- **Track Changes**: Marcas `<w:ins>` y `<w:del>` nativas de Word
- **Preservación de formato**: Negrita, cursiva, etc.
- Control total sobre las correcciones propuestas

## 📦 Instalación

```bash
# Instalar dependencias básicas
pip install -r requirements.txt

# (Opcional) Instalar dependencias profesionales
pip install -r requirements_fase2.txt
```

## 💻 Uso

### Modo Básico (Correcciones Directas)

```bash
# Corrección automática
python main.py documento.docx

# Especificar archivo de salida
python main.py documento.docx -o corregido.docx
```

**Resultado**: Archivo `documento_corregido.docx` con cambios aplicados directamente.

### Modo Profesional (Track Changes)

```bash
# Con Track Changes
python main.py documento.docx --profesional

# Personalizar autor
python main.py documento.docx -p --autor "María García"

# Archivo de salida específico
python main.py documento.docx -p -o revision.docx
```

**Resultado**: Archivo `documento_tc.docx` con marcas de revisión que puedes aceptar/rechazar en Word.

## 🎯 Correcciones Implementadas

### Ortotipografía (RAE)
- ✅ **Comillas**: `"texto"` → `«texto»` (latinas)
- ✅ **Rayas en diálogos**: `- texto` → `—texto` (U+2014)
- ✅ **Espacios duros**: `25 %` → `25 %` (non-breaking)
- ✅ **Puntuación**: `«texto».` (después de comillas)

### Gramática (LanguageTool) *
- ⚠️ Tildes faltantes
- ⚠️ Concordancia de género/número
- ⚠️ Dequeísmo/queísmo

\* *Requiere Java para LanguageTool. Si no está disponible, solo aplica ortotipografía.*

## 📚 Crear Documento de Prueba

```bash
python crear_prueba.py
python main.py documento_prueba.docx --profesional
```

Abre `documento_prueba_tc.docx` en Word → Pestaña **Revisar** → **Control de cambios**

## 🏗️ Arquitectura

```
Modo Básico:
  .docx → python-docx → LanguageTool + Ortotipo → python-docx → .docx

Modo Profesional:
  .docx → ZIP → lxml (XML) → Detección → w:ins/w:del → lxml → ZIP → .docx
```

## 📂 Estructura del Proyecto

```
corrector-ortotipografico/
├── main.py                      # CLI principal (ambos modos)
├── corrector.py                 # Corrector básico
├── corrector_profesional.py     # Corrector con Track Changes
├── ortotipografia.py            # Reglas RAE deterministas
├── xml_handler.py               # Manipulación OpenXML
├── crear_prueba.py              # Generador de documento de prueba
├── requirements.txt             # Dependencias Fase 1
├── requirements_fase2.txt       # Dependencias Fase 2
└── README.md                    # Este archivo
```

## 🎓 Basado en

- **Normativa RAE y ASALE**: Ortografía de la lengua española
- **José Martínez de Sousa**: Manual de estilo de la lengua española
- **Fundéu**: Fundación del Español Urgente
- **ECMA-376**: Office Open XML estándar

## 📝 Notas Técnicas

- **LanguageTool**: Requiere Java. Si no está disponible, modo offline solo ortotipografía
- **Track Changes**: Compatible con Word 2007+
- **Formato XML**: Preserva negrita, cursiva y formato básico
- **Backups**: Siempre guarda en archivo nuevo, nunca sobrescribe

---

**Versión**: 2.0 (Fase Profesional Completa)  
**Autor**: Basado en requerimientos académicos y profesionales

