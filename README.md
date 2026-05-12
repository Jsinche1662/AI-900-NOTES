# 📘 Apuntes Microsoft AI-900

> **Microsoft Certified: Azure AI Fundamentals**
> Estos apuntes fueron tomados mientras estudiaba para la certificación, los he organizado con ayuda de Gemini para poder compartirlos y apoyar a los que quieran obtenerla. 

---

## Tabla de contenidos

- [General](#general)
- [Principios de IA responsable](#principios-de-ia-responsable)
- [AI Vision (Computer Vision)](#ai-vision-computer-vision)
- [Azure AI Document Intelligence (antes Form Recognizer)](#azure-ai-document-intelligence-antes-form-recognizer)
- [LUIS y su sucesor CLU](#luis-y-su-sucesor-clu)
- [NLP (Procesamiento de Lenguaje Natural)](#nlp-procesamiento-de-lenguaje-natural)
- [Bots](#bots)
- [Catálogo rápido de Azure AI Services](#catálogo-rápido-de-azure-ai-services)
- [Knowledge Mining](#knowledge-mining)

---

## General

- Las tres grandes áreas que cubre el examen son: **Machine Learning, Computer Vision y NLP**.
- **Diseñador de Azure ML** (Azure ML Designer): permite arrastrar y soltar módulos para crear modelos sin escribir código.

---

## Principios de IA responsable

Microsoft define **6 principios** de IA responsable que se evalúan en el examen.

### 1. Equidad (Fairness)
Tratar a todos de manera justa. La IA no debe discriminar ni reflejar sesgos.
- **Ejemplo:** Un banco que rechaza créditos por etnia.
- **Solución:** Balancear los datos de entrenamiento para evitar sesgos.

### 2. Fiabilidad y Seguridad (Reliability & Safety)
La IA debe comportarse como se espera, incluso en situaciones complicadas.
- Sistema robusto que prioriza la seguridad humana.
- **Ejemplo:** Un coche autónomo debe saber detenerse antes de chocar.

### 3. Privacidad y Seguridad (Privacy & Security)
Los datos personales tienen que estar protegidos.
- Respetar y proteger los datos privados.
- **Ejemplo:** Borrar nombres o direcciones de la data utilizada (anonimización).

### 4. Inclusión (Inclusiveness)
La IA debe potenciar a todos, incluso a personas con discapacidad.
- No se debe excluir a nadie.
- **Diferencia con equidad:** Equidad es no discriminar por raza o género; inclusión es adaptarse a discapacidades.
- **Ejemplo:** Una app que lee documentos en voz alta para personas con discapacidad visual.

### 5. Transparencia (Transparency)
El funcionamiento de la IA tiene que ser comprensible.
- Los usuarios deben saber que están interactuando con una IA y entender, a grandes rasgos, cómo se toman las decisiones.
- **Ejemplo:** Un chatbot que se presenta como tal; un sistema que, si te niega un crédito, debe explicar por qué.

### 6. Responsabilidad (Accountability)
Los humanos somos responsables de la IA.
- Las personas que diseñan y despliegan el sistema son las responsables.
- **Ejemplo:** Definir el responsable dentro de la empresa que responde por un modelo de IA antes de ser desplegado.

---

## AI Vision (Computer Vision)

Recordar que **se usan modelos preentrenados** (no se entrenan, solo se usan). También se pueden generar modelos propios con **Custom Vision**. Dentro del servicio también está incluido **OCR** para el reconocimiento de caracteres.

### Detección de caras

- **Computer Vision** tiene detección de caras (bounding box), pero **es diferente al servicio Azure AI Face** (que reconoce e indica de quién es la cara).
- **Azure AI Face** tiene dos modos:
  - **Verificación:** Comprueba si una persona es quien dice ser (1 a 1).
  - **Identificación:** Asocia una cara a una persona dentro de un grupo (1 a N).
- Para usar Face hay que **registrar** previamente a las personas.
- Face devuelve atributos técnicos como gafas, blur, características del rostro, etc.
- **Ya no devuelve edad ni género** por motivos éticos.

### Modelos de dominio (Domain Models)

AI Vision incluye modelos preentrenados de dominio para celebridades, monumentos (landmarks), etc.

---

## Azure AI Document Intelligence (antes Form Recognizer)

Sirve para **extraer datos estructurados de documentos**. Se pueden usar modelos personalizados (custom) o los preentrenados:

- **Receipts:** Vouchers de pago / boletas.
- **Business cards:** Tarjetas de presentación.
- **Invoices:** Facturas.
- **IDs:** Documentos de identidad.

---

## LUIS y su sucesor CLU

**LUIS (Language Understanding Intelligent Service)** entendía el lenguaje natural y devolvía JSON con la intención y entidades detectadas. Le daba "capacidad lectora" al bot.

- **Enunciado:** "Quiero pedir una pizza grande"
- **Intención:** `pedirComida`
- **Entidades:** `pizza`, `pepperoni`, `grande`, `llevar`

> **LUIS está retirado** y fue reemplazado por **CLU (Conversational Language Understanding)**, basado en transformers. Para FAQs se usa **CQA (Custom Question Answering)**, que reemplazó a **QnA Maker**.

---

## NLP (Procesamiento de Lenguaje Natural)

Recordar: primero **se remueven las stopwords** para obtener el contexto.

Teóricamente NLP abarca tanto texto como voz, pero **Azure lo divide en 2 servicios**:

### Texto → Azure AI Language

Detecta sentimientos, significado, palabras clave, idioma y entidades.

- **NER (Named Entity Recognition):** Devuelve ISO del idioma y score.
- **Entity Linking:** Devuelve enlaces a sitios web (Wikipedia) para desambiguar entidades.
- **Key Phrase Extraction:** Devuelve palabras clave para entender el contexto.
- **Sentiment Analysis vs Opinion Mining:**
  - **Sentiment Analysis:** Da el sentimiento general de la oración.
  - **Opinion Mining:** Segmenta por sustantivo, dando granularidad por aspecto.

### Voz → Azure AI Speech

Procesa audio, hace conversión **voz ↔ texto** y también traduce.

### Conceptos clave dentro de Azure AI Language

- **Embeddings:** Vectorizar palabras para encontrar similitudes (ej. Rey y Reina).
- **Tokenización:** Dividir una frase en palabras o subpalabras (tokens).
- **Stemming:** Cortar palabras hasta su raíz (corriendo → corr).
- **Lematización:** Pasar palabras a su lema o forma base (corriendo → correr).

### Question Answering

**Azure AI Language (Question Answering)** es el "abuelo" de RAG, pero **no tiene creatividad**: ubica el extracto de texto que buscas, pero no genera contenido nuevo. **RAG** sí integra IA generativa para producir respuestas.

---

## Bots

Los bots son **contenedores de IA**. Por sí solos no son inteligentes: el bot recibe el texto y se lo pasa a otros servicios de Azure que sí entienden.

- Los bots **viven en canales** (Teams, Facebook, Slack, etc.). Un mismo bot puede estar en varios canales, no es necesario crear uno por cada canal.
- **Albergar al bot:** `Azure AI Bot Service`.
- **Cerebro:** `Azure OpenAI Service` y/o `Azure AI Language` (que ya soporta RAG).
- **SDK:** Permite escribir el código del bot en **Python o C#**.

Servicio relacionado: **Azure AI Search** para realizar búsquedas sobre datos propios.

>**Nota:** Azure ML Studio incluye **Data Labelling** para etiquetar datos.

---

## Catálogo rápido de Azure AI Services

### Decisión

- **Anomaly Detector:** Identifica problemas potenciales de manera temprana.
- **Content Moderator:** Detecta contenido potencialmente ofensivo o no deseado.
- **Personalizer:** Crea experiencias personalizadas para cada usuario.

### Lenguaje (Language)

- **Language Understanding (LUIS / CLU):** Incorpora la comprensión de lenguaje natural en aplicaciones, bots y dispositivos IoT.
- **QnA Maker:** (Antigua) crear una capa conversacional de preguntas y respuestas sobre tus datos. Reemplazada por **Custom Question Answering**.
- **Text Analytics:** Detecta sentimientos, frases clave y entidades nombradas.
- **Translator:** Detecta y traduce más de 90 idiomas soportados.

### Voz (Speech)

- **Speech to Text:** Transcribe el habla en texto legible y con capacidad de búsqueda.
- **Text to Speech:** Convierte texto en habla realista para interfaces más naturales.
- **Speech Translation:** Integra traducción de voz en tiempo real (S2T → Translator → T2S).
- **Speaker Recognition:** Identifica y verifica a las personas que hablan a partir del audio.

### Visión (Vision)

- **Computer Vision:** Analiza contenido en imágenes y video.
- **Custom Vision:** Personaliza el reconocimiento de imágenes para tu negocio.
- **Face:** Detecta e identifica personas y emociones en imágenes.

---

## Knowledge Mining

Consiste en **aprender desde una vasta cantidad de información**. Tiene 3 fases:

1. **Ingesta:** Cargar archivos (estructurados o no).
2. **Enriquecimiento (cognitivo):** Aplicar servicios de IA para extraer entidades, traducir, hacer OCR, etc.
3. **Exploración:** Consumir la información desde aplicaciones de negocio (Power BI, apps custom, etc.).

---

