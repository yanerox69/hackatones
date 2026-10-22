# Resultados y recomendaciones del jurado

Datos tomados de las páginas públicas de lablab (última revisión: 22 de octubre de 2026).

**Ganadores:** ninguno de los cuatro hackathones tiene ganadores publicados todavía
(la lista `winners` de cada página de resultados está vacía). Las cuatro entregas
figuran como `OTHER`, es decir, sin puesto asignado por ahora.

**Clasificación por puntos:** la página *Results* de cada hackathon muestra una
tabla de puntos por participante (actividad en el evento: entrega, likes, reseñas).
No es el veredicto del jurado, pero da una idea de visibilidad.

| # | Hackathon | Proyecto | Nota media del jurado | Puesto en la tabla de puntos | Likes |
|---|---|---|---|---|---|
| 01 | AssemblyAI — Voice Agent | RevenueFlow | **4,25 / 5** (2 jueces) | 79 de 200+ (157 pts) | 2 |
| 02 | IBM Bob 2.0 | Issue → PR | **3,0 / 5** (2 jueces) | fuera del top 200 | 0 |
| 03 | WeAreDevelopers × BAND | Dark Factory | sin nota numérica (4 jueces, 2 con comentario) | **14** de 200 (165 pts) | 6 |
| 04 | AMD Developer Hackathon: ACT III | DocuSwarm | **3,6 / 5** (2 jueces) | 48 de 200 (165 pts) | 6 |
| 05 | AMD AI League | DocuSwarm | abierto hasta el 1 dic | — | — |

---

## 01 · RevenueFlow — AssemblyAI Voice Agent Hackathon

| Juez | Valor de negocio | Originalidad | Presentación | Uso de la tecnología |
|---|---|---|---|---|
| Andrii Stetsenko | 4 | 4 | 4 | 4 |
| Ansh Bilimoria | 5 | 4 | 4 | 5 |
| **Media** | **4,5** | **4,0** | **4,0** | **4,5** |

**Lo que valoraron:** la frontera entre lo que decide el modelo y lo que decide el
sistema está aplicada en el código, no solo descrita (esquema Zod con enums estrictos,
`sanitizeIntent()` contra el catálogo real, el modelo devuelve un día de la semana y no
una fecha). 180 aserciones en 15 archivos de test. Los paquetes por país (VE/BR) están
bien abstraídos. Las respuestas con plantillas escritas a mano eliminan alucinaciones.
La demo está en vivo y funciona.

**Lo que criticaron:**
1. Un único `WHATSAPP_ACCESS_TOKEN` contradice el discurso de multi-tenant.
2. El repo deriva de un proyecto anterior con el mismo stack.
3. No hay monitoreo de salud, y el envío por WhatsApp descarta mensajes en silencio cuando no hay número conectado.
4. Las slides citan cifras de penetración de WhatsApp sin fuente.

**Recomendación explícita del jurado:** añadir una cola de mensajes no entregados
(*dead-letter queue*) y credenciales de WhatsApp por cliente en vez de un token único.

**Mi recomendación:**
- Arreglar los 4 puntos: token por tenant, cola de no entregados, endpoint `/health`, y quitar o citar la cifra de la slide 3.
- La crítica de "derivado de un proyecto anterior" se responde con la línea de *disclosure* que ya está en la entrega; en próximos hackathons, empezar repo nuevo o marcar claramente qué se hizo dentro del plazo.

---

## 02 · Issue → PR — IBM Bob 2.0 Hackathon

| Juez | Valor de negocio | Originalidad | Presentación | Uso de la tecnología |
|---|---|---|---|---|
| Vedant Sharma | 2 | 2 | 3 | 3 |
| Nalini Garg | 3 | 3 | 4 | 4 |
| **Media** | **2,5** | **2,5** | **3,5** | **3,5** |

**Lo que valoraron:** uso idiomático de Bob 2.0 (modos personalizados, subtareas,
subagentes `explore`, restricciones `fileRegex` que impiden físicamente al Fixer tocar
los tests). La evaluación con tests ocultos (9/10, ~2 Bobcoins por arreglo) es rigurosa,
y reportar honestamente el fallo suma credibilidad.

**Lo que criticaron:**
1. Automatizar de bug a PR no es una idea nueva.
2. La evaluación usa bugs sembrados en una sola librería Python: queda abierta la pregunta de si funciona en repos reales.

**Mi recomendación:**
- Es la nota más baja, y el problema es **valor de negocio y originalidad**, no la ejecución.
- Para subirla: correrlo sobre issues reales de 2–3 repos open source y medir cuántos PRs serían aceptables, y presentar un caso de negocio (horas de ingeniería ahorradas por bug, coste en Bobcoins frente a coste de un desarrollador).
- En el pitch, abrir con el problema de negocio, no con la arquitectura.

---

## 03 · Dark Factory — WeAreDevelopers × BAND (pista pocketful)

Cuatro jueces; este hackathon no usa nota numérica. Dos dejaron comentario.

**Bhargavi Vepuri:** demuestra colaboración real entre agentes con roles separados
(coordinador, implementador, revisor), un checklist de 158 ítems y 147 checks pasados;
coste y métricas bien documentados. **Pero** dos defectos escaparon a la revisión y
necesitaron intervención humana (incluido un fallo de login), y hay poca evidencia de
una interfaz pulida. *"La verificación autónoma incompleta y la poca evidencia de una
interfaz de usuario pulida impiden una puntuación más alta."*

**Anil Mandloi:** resume el proyecto y destaca que el revisor atrapó un bug de dinero
antes de escribir código, y cierra con *"An honest factory, with the miss written down"*
(una fábrica honesta, con el fallo por escrito).

**Puesto 14 en la tabla de puntos**, el mejor de tus cinco entregas, en un hackathon
con más de 190 participantes.

**Mi recomendación:**
- La debilidad señalada es exactamente la que tú mismo documentaste: el revisor se apagó para ahorrar presupuesto. En una próxima edición, presupuestar el revisor como obligatorio y no como opcional.
- Mostrar la interfaz web del servicio en el video, no solo la sala de agentes.
- La honestidad sobre los fallos fue bien recibida: mantener ese estilo.

---

## 04 · DocuSwarm — AMD Developer Hackathon: ACT III

| Juez | Valor de negocio | Originalidad | Presentación | Uso de la tecnología |
|---|---|---|---|---|
| Juez 1 | 3 | 2 | 3 | 3 |
| Juez 2 | 5 | 4 | 4 | 5 |
| **Media** | **4,0** | **3,0** | **3,5** | **4,0** |

**Juez 1 (el más duro):** buena forma de mostrar el rendimiento de la GPU AMD (agentes
asíncronos, hasta 20 contratos contra un solo endpoint vLLM, panel en vivo, exportación
Excel/JSON). Debilidades: **no hay archivo de licencia**, **la demo es una IP en HTTP**, y
las herramientas de revisión de riesgo en documentos son una categoría saturada con poco
nuevo. Mejoraría con cifras de precisión o de rendimiento. Aclara que no ejecutó el código
ni vio el video.

**Juez 2 (el más favorable):** el proyecto encaja muy bien con el reto de AMD y convierte el
rendimiento de la GPU en una función visible del producto, no en una dependencia de fondo.
El resultado en la MI300X (6 documentos en 1,5 s a 1.653,9 tokens/s) es evidencia concreta
de hardware, y el diseño compatible con OpenAI hace práctico el despliegue. **La demo por IP
no respondió durante la revisión**, así que no pudo probar el panel. Para uso real en
empresas faltarían citas a la fuente, evidencia por página, validación de la extracción y
controles de revisión legal. Concluye que centrar el proyecto en el *continuous batching*,
la telemetría de concurrencia y el rendimiento medido en AMD lo hace *"una implementación
sólida y diferenciada"*.

**Mi recomendación para la AMD AI League (cierra el 1 dic):**
1. ✅ **Hecho (22 oct):** licencia MIT añadida al repo `docuswarm`.
2. ✅ **Hecho (22 oct):** demo pública con HTTPS en https://yanerox69.github.io/docuswarm/ (modo demo en el navegador, sin GPU, con 8 contratos de ejemplo).
3. ◐ **En parte (22 oct):** `backend/bench.py` y tabla 1x/2x/4x/8x en el README con el proveedor *mock* (8x = 6,0x más rápido que 1x). Falta repetirla en GPU y medir precisión.
4. Para subir valor de negocio: mostrar la cláusula exacta (página y texto) que justifica cada alerta.

---

## Patrones en todas las reseñas

| Lo que suma puntos | Lo que resta |
|---|---|
| Garantías aplicadas en el código, no prometidas | Ideas que el jurado ya ha visto |
| Medición honesta, incluidos los fallos | Afirmaciones sin fuente (cifras de mercado) |
| Demo en vivo que funciona | Demo caída o que necesita humano (2 de 4 proyectos) |
| Tests y métricas concretas | Contradicciones entre el discurso y el código |

**Para Airlock y lo que venga:** abrir con el problema de negocio, mantener la demo
viva durante toda la evaluación, citar o quitar cualquier cifra externa, y seguir
documentando los fallos: es lo que más elogios ha recibido.
