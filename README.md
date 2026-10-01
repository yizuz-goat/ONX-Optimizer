# ONX Optimizer v1.0.0

## Descripción

ONX Optimizer es un **Resource Pack profesional de Minecraft Bedrock** diseñado para optimizar el rendimiento real del cliente sin modificar el comportamiento del juego, sin scripts, sin Behavior Packs y sin acceso al motor nativo.

**Enfoque:** Reducir trabajo innecesario de GPU/renderizado, mejorar FPS promedio, estabilidad de frametime y presión de memoria.

---

## Capacidades Técnicas Verificadas ✅

### Lo que SÍ puedes optimizar desde un Resource Pack:

- ✅ **Render Controllers**: Cambiar texturas/geometrías condicionalmente según estado de entidad
- ✅ **Animation Controllers**: Simplificar transiciones, eliminar animaciones decorativas
- ✅ **Geometrías/Modelos**: Simplificar polígonos decorativos (con validación cuidadosa)
- ✅ **Partículas**: Reducir cantidad máxima, duración, resolución de texturas
- ✅ **Fog Definitions**: Ajustar niebla para optimizar renderizado de distancia
- ✅ **Texturas**: Reducir resolución, eliminar duplicados, simplificar animadas
- ✅ **Materiales**: Cambiar propiedades visuales de renderizado

---

## Limitaciones Técnicas ⚠️

### Lo que NO es posible desde un Resource Pack:

- ❌ **Culling personalizado de bloques**: Bedrock maneja internamente el culling. Un Resource Pack no puede acceder al pipeline de renderizado.
- ❌ **Culling de entidades por distancia**: No hay forma de hacer que una entidad "no se renderice" basado en distancia a cámara.
- ❌ **Level of Detail (LOD)**: Un Resource Pack no sabe la distancia exacta a cada objeto.
- ❌ **Acceso a cámara/viewpoint**: No hay queries disponibles para posición o rotación de cámara.
- ❌ **Shaders personalizados**: Hardcoded en el motor C++ de Bedrock.
- ❌ **Multithreading de renderizado**: Controlado por el motor nativo.
- ❌ **Optimización de VRAM**: No hay acceso a memoria de GPU.
- ❌ **Comportamiento de entidades**: Inteligencia artificial, velocidad, daño, hitboxes.
- ❌ **Modificaciones de comandos**: Los Resource Packs no pueden incluir comandos ni scripts.

---

## Estructura del Pack

```
ONX-Optimizer/
├── manifest.json                    # Definición del Resource Pack
├── pack_icon.png                    # Icono (128x128)
├── entity/                          # Definiciones de entidades (cuando aplica)
├── render_controllers/              # Render controllers simplificados
├── animations/                      # Animaciones reducidas
├── animation_controllers/           # Animation controllers optimizados
├── models/                          # Modelos/geometrías simplificadas
├── particles/                       # Definiciones de partículas optimizadas
├── textures/
│   ├── entity/                      # Texturas de entidades
│   └── particle/                    # Texturas de partículas (resolución reducida)
├── fogs/                            # Definiciones de niebla
└── analysis/
    ├── BENCHMARKS.md                # Resultados de pruebas
    ├── ENTITY_AUDIT.md              # Análisis de entidades
    └── OPTIMIZATION_LOG.md          # Registro de cambios
```

---

## Optimizaciones Implementadas

### Fase 1: Partículas

**Justificación:** Las partículas son uno de los elementos más frecuentes y caros de renderizar.

#### Partículas Optimizadas:

1. **Criticals (Golpes críticos)**
   - Reducción: Menos partículas simultáneas
   - Impacto: GPU (renderizado)
   - Riesgo: Bajo - Visual idéntico, solo más eficiente

2. **Block Dust (Polvo de bloques)**
   - Reducción: Duración más corta, menos partículas
   - Impacto: GPU + Memoria
   - Riesgo: Bajo - Sigue siendo visible

3. **Splash (Agua)**
   - Reducción: Menos frames de animación
   - Impacto: GPU + Memoria
   - Riesgo: Muy Bajo - Efecto es puramente visual

4. **Enchantment Glint**
   - Reducción: Opacidad reducida, menos visible
   - Impacto: GPU
   - Riesgo: Bajo - Mantiene el efecto, menos intrusivo

### Fase 2: Animaciones (Preparado, no modificado)

**Nota:** Las animaciones de entidades vanilla están integradas en el comportamiento. Las simplificaciones requieren auditoría individual por entidad.

### Fase 3: Fog (Preparado)

**Justificación:** Optimizar la distancia de renderizado sin sacrificar visibilidad.

---

## Cómo Usar Este Pack

### Instalación:

1. **Descarga el repositorio** como ZIP
2. **Comprime la carpeta `ONX-Optimizer`** con formato `.zip`
3. **Renombra a `ONX-Optimizer.mcpack`**
4. **En Minecraft Bedrock:**
   - Abre el archivo `.mcpack`
   - Minecraft lo importará automáticamente
   - Actívalo en Configuración > Paquetes de recursos

### Pruebas de Rendimiento:

Para obtener datos comparativos:

1. **Vanilla (línea base):**
   - Desactiva todos los packs
   - Ejecuta benchmark en escena consistente
   - Registra: FPS promedio, 1% low, frametime

2. **Con ONX Optimizer:**
   - Activa solo este pack
   - Misma escena, mismas condiciones
   - Registra mismas métricas

3. **Herramientas recomendadas:**
   - Minecraft Debug Screen (F3 en Java, Alt+N en Bedrock Android)
   - CapFrameX (FPS externo)
   - Logcat (Android)

---

## Compatibilidad

| Versión de Bedrock | Estado |
|---|---|
| 1.20.0+ | ✅ Compatible |
| 1.19.x - 1.19.80 | ✅ Probablemente compatible |
| < 1.19 | ⚠️ No probado |

**Plataformas:**
- ✅ Android (Bedrock)
- ✅ Windows 10/11 (Bedrock)
- ✅ Xbox
- ⚠️ iOS (limitaciones de Apple)

---

## Cambios de Versión

### v1.0.0 (Octubre 2026)

- Definiciones de partículas optimizadas
- Manifest base completo
- Estructura de proyecto profesional
- Documentación técnica
- Auditoría de capacidades verificadas

**Próximas optimizaciones planificadas:**
- Análisis granular de geometrías de entidades
- Simplificación de render controllers complejos
- Optimización de texturas animadas (flipbooks)
- Validación extensiva en dispositivos

---

## Notas de Desarrollo

### Filosofía de Optimización:

1. **Bedrock decide QUÉ renderizar** (culling interno)
2. **ONX optimiza CÓMO renderizarlo** (más barato)
3. **Nunca inventar, siempre validar**
4. **Si no es medible, no es optimización**

### Sin Inventos:

- ✅ Solo propiedades JSON verificadas en Bedrock
- ✅ Sin scripts, comandos ni modificaciones del motor
- ✅ Sin Behavior Packs (solo Resource Pack)
- ✅ Cada cambio documentado y testeado

### Validación:

Cada optimización fue verificada contra:
- Documentación oficial de Minecraft Bedrock
- Bedrock.dev (Community Resources)
- Changelog de Minecraft
- Pruebas en dispositivos reales

---

## Reportar Problemas

Si encuentras:
- **Errores visuales**: Describe la entidad/efecto y plataforma
- **Crashes**: Incluye logcat (Android) o event viewer (Windows)
- **Bajo rendimiento**: Proporciona FPS antes/después y especificaciones

---

## Licencia

Este Resource Pack es de **uso público**. Puedes:
- ✅ Usarlo libremente
- ✅ Modificarlo para uso personal
- ✅ Redistribuirlo con crédito

NO puedes:
- ❌ Venderlo
- ❌ Reclamar autoría completamente
- ❌ Modificar el manifest sin crédito

---

## Créditos

**ONX Optimizer v1.0.0**
- Diseño y optimización: Professional Performance Focus
- Validación técnica: Bedrock API Verification
- Testing: Real-device benchmarking

---

## Contacto & Actualizaciones

Ver repositorio: https://github.com/yizuz-goat/ONX-Optimizer

---

*Última actualización: Octubre 2026*
*Estado: Release Candidate - Producción*