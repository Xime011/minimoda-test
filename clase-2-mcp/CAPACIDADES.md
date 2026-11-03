# Capacidades y límites de los MCP

## Playwright MCP

Codex abrió MiniModa, seleccionó el Body Manga Larga Estrellitas
en color azul y talle 6M, lo agregó al carrito y verificó que
apareciera por $8.500. También guardó las capturas de la tienda
y del carrito. El turno duró 1 min 17 s.

## MCP de casos de prueba

Usé `crear_caso_prueba` para generar un caso de prioridad alta
sobre agregar un producto con stock al carrito. La herramienta
guardó el caso en Markdown y `listar_casos` confirmó que el
archivo estaba disponible. El turno completo duró 2 min 41 s.

## Comparación con el trabajo manual

Estimo que hacer el recorrido, guardar las capturas y redactar
el caso a mano me habría llevado unos 10 minutos en total.
Los dos turnos de Codex sumaron 3 min 58 s una vez que los MCP
estaban disponibles. La primera práctica completa me llevó más
tiempo que hacer esas tareas a mano porque tuve que entender
la consigna, aprender el flujo y configurar las herramientas.
No cronometré la preparación completa.

## Límites observados

Codex pudo crear el código del servidor, pero su entorno bloqueó
la instalación de dependencias y el registro del MCP. Completé
ambos pasos desde PowerShell. La instalación tardó 9 segundos,
medidos aparte de la generación del caso. También revisé las
capturas y el Markdown antes de preparar la entrega.