Editor Literario Local - Documentacion Tecnica

1. Descripcion General y Arquitectura
El Editor Literario Local es una aplicacion web de archivo unico (.html) desarrollada integramente con tecnologias del lado del cliente (HTML5, JavaScript ES6+ y CSS3 / Tailwind CSS). Su arquitectura se basa en el procesamiento asincrono local, eliminando la necesidad de un servidor backend persistente para las funciones de analisis estadistico, procesamiento de archivos y generacion de grafos.Caracteristicas Principales
Procesamiento Heuristico Local: Analisis lexico y estadistico ejecutado directamente en el hilo principal o mediante Web Workers, garantizando la privacidad absoluta del texto procesado.
Soporte de Formatos: Incorporacion de la biblioteca Mammoth.js para la extraccion y conversion directa de documentos binarios de Microsoft Word (.docx) a texto estructurado en el DOM.
Integracion con Modelos de Lenguaje (LLM): Capacidad de conexion bidireccional mediante llamadas HTTP asincronas (fetch API) con la API de Google Gemini, instancias locales de Ollama o endpoints compatibles con la interfaz de OpenAI.
Visualizacion Dinamica: Generacion de grafos de relaciones entre personajes basados en vectores SVG manipulados mediante DOM nativo y metricas de co-ocurrencia por capitulo.

2. Requisitos Previos e Instalacion
Al tratarse de una aplicacion estatica autocontenida, no requiere la instalacion de entornos de ejecucion complejos como Node.js, gestores de bases de datos o servidores de aplicaciones dedicados para su funcionamiento basico.

Requisitos del Sistema
Navegador web moderno con soporte para ECMAScript 6+, Fetch API y manipulacion avanzada del DOM (Google Chrome, Mozilla Firefox, Microsoft Edge, Apple Safari).
Opcional (para auditorias neuronales locales): Instancia de Ollama ejecutandose localmente (por defecto en http://localhost:11434) con los modelos requeridos descargados (ej. llama3, mistral).
Opcional (para auditorias en la nube): Credencial de acceso (API Key) valida para Google Gemini.

Puesta en Marcha
Clonar o descargar el repositorio fuente que contiene el archivo unico de la aplicacion (ej. index.html).
Debido a las politicas de seguridad del navegador (CORS) y la carga de modulos externos mediante CDN, se recomienda encarecidamente ejecutar la aplicacion mediante un servidor de desarrollo local:
Visual Studio Code: Instalar la extension Live Server, hacer clic derecho sobre el archivo HTML y seleccionar la opcion Open with Live Server.
Python (Alternativa CLI): Ejecutar python3 -m http.server 8000 en el directorio raiz y acceder a http://localhost:8000 desde el navegador.
Alternativamente, para pruebas rapidas sin carga de recursos externos complejos, se puede arrastrar y soltar el archivo directamente en la ventana del navegador.

3. Configuracion y Parametros de Analisis
El motor de analisis se divide en dos fases: un analisis heuristico determinista y una auditoria probabilistica opcional basada en modelos de lenguaje.
Segmentacion y Metricas Lexicas
Segmentacion por Bloques: El texto de entrada se divide de forma automatica utilizando expresiones regulares que identifican saltos de linea dobles y patrones de marcado de capitulos (Capitulo, Chapter, Numeracion Romana).
Deteccion de Dialogos: Identificacion sintactica basada en el uso de raya de dialogo (—), comillas latinas («») e inglesas ("") para calcular la proporcion dialogica frente a la narrativa.
Conteo Lexico: Analisis de densidad adverbial (terminaciones en -mente), frecuencia de gerundios, calculo de tiempo estimado de lectura y variabilidad en la longitud de las oraciones para medir el ritmo narrativo.

Parametros de IA y Grafos de Relaciones
Ajuste de Temperatura: Control del parametro estocastico del LLM (rango sugerido de 0.2 a 0.7) para equilibrar la creatividad en las sugerencias de estilo con la rigurosidad tecnica en la deteccion de contradicciones argumentales.
Perfiles Psicologicos: Extraccion estructurada mediante esquemas JSON estrictos devueltos por el modelo para mapear la evolucion de los personajes a lo largo del manuscrito.
Grafos SVG: Construccion de matrices de adyacencia basadas en la aparicion conjunta de entidades nominales dentro de los mismos bloques de texto, renderizadas de manera dinamica en coordenadas cartesianas vectoriales.

4. Estructura de Modulos y Funciones Principales
El codigo fuente esta estructurado dentro del mismo archivo HTML mediante modulos de script embebidos y logica procedural orientada a eventos:
Modulo de Ingesta (MammothIntegration): Gestiona la lectura de archivos .docx, convirtiendo los flujos de bytes en cadenas de texto plano preservando las etiquetas estructurales basicas.
Motor Estadistico (TextHeuristics): Agrupa funciones puras encargadas del calculo de indices de legibilidad, densidad de vocabulario, repeticiones lexicas y deteccion de muletillas o redundancias argumentales.
Cliente LLM (LLMBridge): Abstrae las peticiones HTTP hacia la API de Gemini o el servidor local de Ollama. Gestiona los encabezados de autenticacion, el manejo de errores por tiempo de espera (timeout) y la deserializacion de respuestas estructuradas en formato JSON.
Renderizador de Grafos (SVGGraphEngine): Calcula dinamicamente los nodos y aristas del sistema de relaciones literarias, aplicando algoritmos basicos de posicionamiento para evitar solapamientos visuales.

5. Instrucciones de Uso
Carga de Manuscrito: Utilice el selector de archivos para cargar un documento .docx, .txt, .md o pegue el contenido directamente en el area de texto designada en la interfaz principal.
Ejecucion del Analisis Local: Haga clic en el boton de procesamiento estadistico para generar los metadatos de lectura, graficas de ritmo y deteccion preliminar de entidades.
Configuracion de Auditoria Neuronal: Si desea una revision de estilo o continuidad argumental, seleccione el proveedor de LLM deseado, introduzca el endpoint o la clave de API correspondiente y establezca el contexto o la guia de estilo del manuscrito.
Revision Interactiva: Navegue a traves de las alertas generadas en el panel lateral para aplicar modificaciones sugeridas directamente sobre el texto fuente.

