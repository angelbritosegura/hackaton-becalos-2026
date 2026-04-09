# FlotaIA · Panel de Mantenimiento Predictivo de Flota

> **Becalos Hackaton 2026 · EJE 3: Prevención y Disponibilidad**

Prototipo web estático de un panel de mantenimiento predictivo para flotas de transporte público, desarrollado como solución al EJE 3 del hackaton.

---

## 📁 Estructura del Proyecto

```
hackaton-becalos-2026/
├── index.html   # Interfaz principal del panel predictivo
├── style.css    # Estilos (tonos morado, gris y blanco)
└── README.md    # Documento ejecutivo del proyecto
```

---

## 🚨 Problema Operativo

Las flotas de transporte público en México enfrentan pérdidas millonarias debido a fallas mecánicas inesperadas que generan:

- **Paros no programados** que sacan unidades de circulación durante horas o días.
- **Alto costo de reparaciones correctivas** (hasta 3× el costo de mantenimiento preventivo).
- **Riesgo para pasajeros y operadores** por fallas en componentes críticos (motor, frenos, suspensión).
- **Impacto en la calidad del servicio** y tiempos de espera para los usuarios.

El diagnóstico actual depende de la experiencia empírica del mecánico y de revisiones periódicas fijas, sin considerar el estado real de cada unidad ni sus condiciones de operación específicas.

---

## 🤖 Lógica del Modelo de IA

El panel visualiza la salida de un modelo de **mantenimiento predictivo** basado en las siguientes etapas:

1. **Ingesta de datos**: Se recopilan en tiempo real el kilometraje acumulado, los códigos de falla OBD-II (P, B, C, U), las condiciones de operación (tipo de ruta, temperatura ambiente, nivel de carga) y el historial de mantenimiento previo.

2. **Procesamiento y normalización**: Los datos crudos son limpiados y normalizados para eliminar valores atípicos y llenar vacíos con promedios históricos de unidades similares.

3. **Modelo de clasificación de riesgo**: Un clasificador (Random Forest o Gradient Boosting) entrenado con datos históricos de fallas asigna a cada unidad una **probabilidad de falla en los próximos N días** y la clasifica en tres niveles:
   - 🟢 **Verde (Bajo)** — Probabilidad < 40 %. Sin acción inmediata requerida.
   - 🟡 **Amarillo (Medio)** — Probabilidad 40–75 %. Revisión programada en ≤ 3 días.
   - 🔴 **Rojo (Alto)** — Probabilidad > 75 %. Retiro inmediato de circulación.

4. **Generación de recomendaciones**: Con base en los códigos de falla activos y el nivel de riesgo, el sistema sugiere acciones específicas (componentes a inspeccionar, tiempo estimado de intervención).

5. **Visualización**: Los resultados se presentan en el panel mediante el **Semáforo de Riesgo** y la tarjeta de **Acción Sugerida**.

---

## 📈 Impacto Esperado

| Indicador | Situación actual | Con FlotaIA |
|---|---|---|
| Paros no programados | ~18 % de la flota/mes | Reducción estimada al 6 % |
| Costo de mantenimiento correctivo | Alto (reactivo) | Reducción del 40–60 % |
| Disponibilidad de flota | ~82 % | Meta ≥ 94 % |
| Tiempo de diagnóstico por unidad | 2–4 h (manual) | < 5 min (automatizado) |
| Vida útil promedio de unidades | Línea base | Incremento estimado 15 % |

---

## ⚠️ Limitaciones

- **Datos de entrenamiento**: El modelo requiere un historial mínimo de 12–18 meses de datos de fallas por tipo de unidad. Flotas pequeñas o nuevas pueden tener baja precisión inicial.
- **Calidad de los sensores OBD-II**: Unidades antiguas sin puerto OBD estándar no pueden proveer códigos de falla en tiempo real, limitando la cobertura del sistema.
- **Conectividad**: El prototipo actual es estático; la integración con sensores en tiempo real requiere infraestructura de IoT y conexión de datos en las unidades.
- **Mantenimiento del modelo**: El clasificador debe reentrenarse periódicamente (cada 3–6 meses) para evitar degradación por deriva de distribución (*data drift*).
- **Factores externos no modelados**: Condiciones climáticas extremas, accidentes o modificaciones no documentadas en las unidades pueden generar falsos negativos.

---

*Desarrollado por Angel Brito Segura, Juan Pablo Jacobo Estrada & Samuel Frias Contreras*
