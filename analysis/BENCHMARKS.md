# ONX Optimizer - Benchmarks y Validación

## Metodología de Benchmarking

Para garantizar mediciones válidas:

1. **Entorno consistente** (misma escena, tiempo, condiciones climáticas)
2. **10 ejecuciones mínimo** por configuración
3. **Eliminación de outliers** (primer y último ejecutable)
4. **Medición de:** FPS promedio, 1% low, frametime, memoria
5. **Herramientas:** Debug screen nativo + software externo

---

## Configuración de Referencia

### Dispositivo Recomendado para Testing
- **CPU:** Snapdragon 888+ (Android) o Intel i7 10th gen (Windows)
- **GPU:** Adreno 660 (Android) o RTX 2080 (Windows)
- **RAM:** 8GB mínimo (12GB recomendado)
- **Almacenamiento:** SSD

### Escena de Prueba Sugerida

**Ubicación:** Llanura vanilla, sin modificaciones
**Render Distance:** 16 chunks (estándar)
**Gráficos:** Máximo (Farlands OFF, raytracing OFF)
**Entidades:** 20 zombies en área 50x50 bloques
**Condiciones climáticas:** Sol (sin lluvia/tormenta)
**Duración:** 3 minutos mínimo por ejecución

---

## Resultados Baseline (v1.0.0 - Preliminary)

### Estado Actual

**⚠️ NOTA:** Los benchmarks finales serán completados después de validación en dispositivos reales.

Esta sección será actualizada con datos reales cuando estén disponibles.

### Placeholders para Medición

```
Vanilla Baseline (Minecraft Bedrock 1.20.0):
- FPS Promedio: [PENDING TEST]
- FPS 1% Low: [PENDING TEST]
- Frametime Promedio: [PENDING TEST]
- Frametime Max: [PENDING TEST]
- RAM Utilizada: [PENDING TEST]
- VRAM Estimada: [PENDING TEST]

Con ONX Optimizer:
- FPS Promedio: [PENDING TEST]
- FPS 1% Low: [PENDING TEST]
- Frametime Promedio: [PENDING TEST]
- Frametime Max: [PENDING TEST]
- RAM Utilizada: [PENDING TEST]
- VRAM Estimada: [PENDING TEST]

Mejora Neta:
- FPS: [PENDING CALCULATION]
- Estabilidad: [PENDING CALCULATION]
```

---

## Escenarios de Prueba Específicos

### Escenario 1: Overworld (Llanura)
**Objetivo:** FPS base en ambiente controlado

- Entities: 20 Zombies
- Weather: Clear
- Time: 12000 (noon)
- Expected impact: Medium (particle optimization)

### Escenario 2: Nether (Bastion)
**Objetivo:** Rendimiento en fog agresivo

- Entities: 10 Piglins + 10 Zombified Piglins
- Weather: Ash particles heavy
- Time: N/A (Nether no tiene ciclo día/noche)
- Expected impact: High (fog optimization)

### Escenario 3: The End (Island)
**Objetivo:** Rendimiento en ambiente vacío

- Entities: 1 Ender Dragon + 5 Endermen
- Weather: Void particles
- Lighting: Dark (end sky)
- Expected impact: Low-Medium (fog optimization)

### Escenario 4: Combat (Heavy Particles)
**Objetivo:** Estabilidad bajo carga de partículas

- Entities: 30 Skeletons, player attacking
- Weather: Rain (particles)
- Expected impact: High (particle optimization)
- Key metric: Frametime stability, 1% low

---

## Herramientas de Medición

### Minecraft Debug Screen
- Android: Alt+N
- Windows Bedrock: No acceso (limitado)
- Xbox: No acceso

**Métricas disponibles:**
- FPS actual
- Distancia de renderizado
- Chunk loading
- Entidades visibles

### Software Externo Recomendado

#### CapFrameX (PC)
- Overlay de FPS en tiempo real
- Gráficos históricos
- 1% low, 0.1% low
- Frametime detallado

#### Logcat (Android)
```bash
adb logcat | grep -i "minecraft\|bedrock"
```
- Warnings y errores
- Crash logs
- Memory allocation

#### Xbox App (Windows)
- Integración con Xbox Game Pass
- Telemetría básica

---

## Validación Post-Instalación

### Checklist de Funcionalidad

- [ ] Pack carga sin errores
- [ ] Minecraft no crash al aplicar
- [ ] Entidades se renderizan correctamente
- [ ] Partículas visibles en combate
- [ ] Fog aplicado correctamente por dimensión
- [ ] No hay texturas púrpura (missing)
- [ ] No hay flickering visual
- [ ] Audio funciona normalmente
- [ ] HUD (vida, hambre, etc.) visible
- [ ] Controles responden normalmente

---

## Datos Esperados vs. Realidad

### Mejora Esperada (Teórica)

Basado en optimizaciones aplicadas:

| Optimización | Impacto Teórico | Confianza |
|---|---|---|
| Partículas (-40%) | +3-8% FPS | Alta |
| Fog (distancia) | +5-15% FPS* | Alta* |
| Render Controller | +1-2% FPS | Media |
| **TOTAL** | **+9-25% FPS** | **Media** |

**\*En escenarios con render distance larga (16+ chunks)*

### Disclaimer Importante

⚠️ **Estos números son estimaciones teóricas.**

La mejora real depende de:
- Hardware específico
- Escena particular
- Render distance actual
- Cantidad de entidades
- Efectos de partículas activos

**En peor caso:** Sin mejora medible
**En mejor caso:** 15-20% mejora en FPS
**Realista:** 5-10% mejora en escenarios típicos

---

## Próximas Pruebas Planeadas

### v1.0.1 (Próximo)
- [ ] Validación en Snapdragon 888+ (Android)
- [ ] Validación en Windows Bedrock
- [ ] Prueba de stress (100+ entidades)
- [ ] Prueba de memoria (monitoring con Logcat)

### v1.1.0
- [ ] Benchmark comparativo completo
- [ ] Optimizaciones de geometría
- [ ] Prueba en Xbox Series X/S
- [ ] Documentación de resultados

---

## Cómo Contribuir con Benchmarks

Si deseas proporcionar datos de tu dispositivo:

1. **Descarga** el pack desde el repo
2. **Instala** en Minecraft Bedrock
3. **Ejecuta** el escenario de prueba (Overworld llanura, 3 min)
4. **Registra:**
   - Dispositivo (modelo exacto)
   - Versión de Bedrock
   - Render distance
   - Gráficos (calidad)
   - FPS promedio y 1% low
   - Frametime (si disponible)
5. **Reporta** como Issue en GitHub

**Formato:**
```
Dispositivo: [modelo]
Bedrock: [versión]
Render Distance: [chunks]
Gráficos: [calidad]

Vanilla:
- FPS: [X]
- 1% Low: [X]
- Frametime: [Xms]

Con ONX:
- FPS: [X]
- 1% Low: [X]
- Frametime: [Xms]

Mejora: [%]
```

---

*Última actualización: Octubre 2026*
*Status: Metodología Completada - Datos Pending*