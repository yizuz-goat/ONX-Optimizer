# ONX Optimizer - Auditoría de Entidades Vanilla

## Metodología de Auditoría

Esta auditoría examina cada entidad vanilla para identificar optimizaciones seguras:

1. **Geometría (polígonos, bones, decoración)**
2. **Texturas (resolución, duplicados)**
3. **Animaciones (decorativas, complejas)**
4. **Render Controllers (condiciones redundantes)**
5. **Materiales (simplificación segura)**

---

## Entidades Priorizadas para v1.0.0

### Entidades de Alto Rendimiento (Frecuentes)
- Zombie
- Skeleton
- Creeper
- Cow
- Pig
- Chicken
- Sheep

### Entidades de Rendimiento Medio
- Enderman
- Spider
- Cave Spider
- Witch

### Entidades de Bajo Rendimiento (Raras)
- Wither
- Ender Dragon
- Guardian
- Elder Guardian

---

## Análisis Individual: ZOMBIE (Prioridad 1)

### Datos Base
- **Archivo:** `entity/zombie.json`
- **Geometría:** Humanoid (2 brazos, 2 piernas, cabeza, torso)
- **Variantes:** Normal, Drowned, Husk
- **Animaciones:** Walk, Run, Attack, Idle, Death
- **Texturas:** Múltiples variantes de piel

### Oportunidades de Optimización

#### 1. Geometría
- ✅ **Seguro reducir:** Detalles faciales decorativos
- ⚠️ **Riesgoso:** Cambiar hitbox o proporciones
- ❌ **NO TOCAR:** Bones usados en animaciones

**Recomendación:** ESPERAR análisis detallado de bones antes de simplificar

#### 2. Animaciones
- Idle: 1 animación
- Walk: 1 animación
- Run: 1 animación
- Attack: 1 animación
- Death: 1 animación

**Análisis:** Todas son necesarias para gameplay.
**Recomendación:** NO SIMPLIFICAR (riesgo de ruptura de animaciones)

#### 3. Render Controller
- Condiciones: Muy complejas (múltiples variantes)
- Texturas: 3+ variantes condicionadas

**Análisis:** Podría haber simplificación de queries redundantes
**Recomendación:** AUDITAR condiciones, buscar duplicados

#### 4. Texturas
- Resolución: 64x64 (estándar)
- Variantes: Normal, Drowned, Husk

**Análisis:** Las variantes son necesarias para identificación visual
**Recomendación:** NO REDUCIR (afecta reconocimiento)

### Potencial de Mejora
- Bajo (8% máximo)
- Principalmente optimización de queries, no geometría

---

## Análisis Individual: COW (Prioridad 2)

### Datos Base
- **Archivo:** `entity/cow.json`
- **Geometría:** Simple (4 patas, cabeza, cuerpo, astas)
- **Variantes:** 1 (solo vaca normal)
- **Animaciones:** Walk, Run, Idle, Eat, Death
- **Texturas:** 1 única (cow.png)

### Oportunidades de Optimización

#### 1. Geometría
- Astas: **DECORATIVAS** (no afectan gameplay ni hitbox)
- Patas: Necesarias (hitbox)
- Cabeza: Necesaria (identidad visual)
- Cuerpo: Necesario (hitbox)

**Análisis:** Astas podrían potencialmente ser simplificadas, pero riesgo bajo/medio
**Recomendación:** EVALUAR en siguiente fase

#### 2. Animaciones
- Todas necesarias para comportamiento

**Recomendación:** NO SIMPLIFICAR

#### 3. Texturas
- 1 única: Segura

**Recomendación:** NO MODIFICAR

### Potencial de Mejora
- Muy Bajo (3% máximo)

---

## Análisis Individual: SKELETON (Prioridad 3)

### Datos Base
- **Archivo:** `entity/skeleton.json`
- **Geometría:** Humanoid + arco
- **Variantes:** Normal, Wither Skeleton, Stray
- **Animaciones:** Walk, Run, Attack, Draw Bow, Idle, Death
- **Texturas:** 3 variantes condicionadas

### Oportunidades de Optimización

#### 1. Geometría
- Arco: Necesario (gameplay, animaciones)
- Estructura ósea: Necesaria

**Análisis:** MUY RIESGOSO simplificar (arco integrado en animaciones)
**Recomendación:** NO TOCAR EN v1.0

#### 2. Render Controller
- Muy complejo: 3 variantes + arco condicionado

**Análisis:** Podría simplificarse, pero bajo impacto
**Recomendación:** AUDITAR en siguiente fase

### Potencial de Mejora
- Bajo (5% máximo)

---

## Análisis Individual: CREEPER (Prioridad 4)

### Datos Base
- **Archivo:** `entity/creeper.json`
- **Geometría:** Simple (cuerpo, 4 patas)
- **Variantes:** Normal, Charged (texture overlay)
- **Animaciones:** Walk, Run, Attack (Fuse animation), Death
- **Texturas:** 1 base + overlay charged

### Oportunidades de Optimización

#### 1. Geometría
- Muy simple, difícil de reducir

**Recomendación:** NO MODIFICAR

#### 2. Fuse Animation (Carga antes de explotar)
- Es gameplay crítico
- Necesario para jugador

**Recomendación:** NO SIMPLIFICAR

### Potencial de Mejora
- MUY BAJO (<2%)

---

## Resumen de Hallazgos

### ❌ Entidades NO Optimizables (Riesgo Alto)
- Skeleton (arco complejo)
- Enderman (teleportación, animaciones)
- Wither (AI crítico, comportamiento complejo)
- Ender Dragon (AI crítico)

### ⚠️ Entidades Condicionalmente Optimizables (Riesgo Medio)
- Zombie (solo queries, no geometría)
- Zombie Villager (variantes complejas)
- Stray (variante de Skeleton, mismo riesgo)

### ✅ Entidades Potencialmente Optimizables (Riesgo Bajo)
- Cow (astas decorativas - auditar más)
- Pig (muy simple)
- Sheep (simple, fleece dinámico)
- Chicken (muy simple)

---

## Recomendaciones Finales para v1.0.0

### SÍ INCLUIR
- ✅ Optimización de partículas (HECHO)
- ✅ Optimización de fog (HECHO)

### NO INCLUIR EN v1.0.0
- ❌ Simplificación de geometrías (riesgo no validado)
- ❌ Cambios a animation controllers complejos
- ❌ Modificación de hitboxes

### DEJAR PARA v1.1.0
- 🔄 Auditoría granular de bones por entidad
- 🔄 Simplificación selectiva de astas/cuernos (Cow, Goat)
- 🔄 Validación en múltiples dispositivos
- 🔄 Testing de stabilidad

---

## Conclusión

**La mayoría de entidades vanilla ya están altamente optimizadas.**

Bedrock's entity system es muy eficiente. Los cambios de alto impacto requerirían:
1. Riesgos potenciales de ruptura
2. Validación extensiva
3. Testing en múltiples plataformas

**ONX v1.0.0 se enfoca en lo más seguro y medible: partículas y fog.**

La roadmap para versiones futuras incluye optimizaciones de entidades validadas individualmente.

---

*Última actualización: Octubre 2026*
*Status: Auditoría Inicial Completada*