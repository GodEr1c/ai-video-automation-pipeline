# 🚀 AI-Powered Video Orchestration & Distribution Pipeline

> **Nota de Privacidad:** Este repositorio es un *showcase* arquitectónico. Por motivos de propiedad intelectual y ventaja comercial, el código fuente completo, los prompts del LLM y las integraciones de API privadas se mantienen en un repositorio cerrado.

## 📌 Resumen del Proyecto
Un pipeline automatizado *end-to-end* construido en Python que ingesta video comercial crudo, utiliza Inteligencia Artificial para estructurar la retención visual, renderiza overlays dinámicos y distribuye el resultado final en 4 plataformas sociales de forma autónoma. Diseñado para escalar la producción de contenido de comercio electrónico eliminando el cuello de botella de la edición manual.

## ⚡ El Problema vs. La Solución
**El Cuello de Botella:** La edición manual de Shorts/Reels comerciales y su publicación multiplataforma consumía aproximadamente 7.5 horas semanales. El proceso requería recortar silencios, animar subtítulos, agregar elementos de retención visual y gestionar subidas propensas a errores.

**La Solución:** Un orquestador local que:
1. **Limpia el audio/video:** Detecta y recorta silencios automáticamente.
2. **Inyecta Retención Visual:** Usa un LLM para analizar la transcripción y generar "cues" visuales precisos (animaciones Pixel-Art, UI Mockups, transiciones).
3. **Renderiza Nativamente:** Combina motores web y FFmpeg para estampar gráficos dinámicos y subtítulos de alta conversión sin abrir Premiere o CapCut.
4. **Distribuye Autónomamente:** Sube el material renderizado a YouTube Shorts, Facebook Reels e Instagram Reels, notificando el éxito vía Telegram.

## 🛠️ Arquitectura y Stack Tecnológico
* **Core & Orquestación:** Python 3, SQLite (Control de estado y reintentos).
* **Procesamiento de Video:** FFmpeg (Manipulación de A/V, recorte de silencios).
* **Motor Gráfico y UI:** Playwright, GSAP (Renderizado de overlays HTML/CSS invisibles que se estampan en el video).
* **Inteligencia Artificial:** Google Gemini API (Extracción semántica, generación de títulos virales y selección de assets visuales).
* **Distribución:** Meta Graph API, YouTube Data API, Telegram Bot API.

  ```mermaid
  graph TD
    %% Nodos iniciales
    A[📁 Carpeta de Entrada<br>Videos Crudos .MOV] -->|Watchdog / Cron| B(Script 1: Core de Edición)
    
    %% Flujo de Edición (video-automation-core)
    subgraph Orquestador de Video
        B --> C{🧠 Análisis de IA<br>Gemini API}
        C -->|Genera| D[JSON Cues Visuales & Títulos]
        C -->|Transcribe| E[Chunker de Subtítulos]
        D --> F[Motor de Renderizado<br>Playwright + GSAP]
        E --> F
        F --> G[Ensamblaje FFmpeg<br>Cortes, Punch-In y Overlays]
    end

    %% Flujo de Distribución (Automatizador de contenido)
    G -->|Exporta .mp4 + .txt| H(Script 2: Distribuidor Multiplataforma)
    
    subgraph Pipeline de Distribución
        H --> I[(SQLite<br>Control de Estado)]
        I -->|Verifica Duplicados| J{APIs de Redes Sociales}
        J -->|Subida| K[YouTube Shorts]
        J -->|Subida| L[Instagram Reels]
        J -->|Subida| M[Facebook Reels]
    end

    %% Notificación
    J -->|Webhook / API| N[📱 Telegram Bot<br>Alerta de Éxito y Links]
  ```
      

## 📈 Impacto y ROI Operativo
* **Ahorro de Tiempo:** Reducción de la carga de trabajo manual de ~30 minutos por video (edición y subida multiplataforma) a **menos de 60 segundos de procesamiento computacional**.
* **Escalabilidad:** Permite procesar y distribuir un promedio de 60-90 Shorts mensuales ahorrando más de **30 horas netas de trabajo operativo al mes**.
* **Mejora Cualitativa:** La edición automatizada superó la complejidad de la edición manual anterior (que se limitaba a cortes de silencio), inyectando ahora componentes de alta retención (UI mockups, Pixel-Art y animaciones) con costo de tiempo cero.
* **Distribución Garantizada:** Sistema idempotente que asegura la presencia de la marca simultáneamente en YouTube, Facebook e Instagram sin intervención humana tras depositar el crudo.
