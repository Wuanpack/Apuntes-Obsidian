REMnux Vm es una distribución especializada de Linux. Incluye herramientas como Volatility, YARA, Wireshark, oledump e INetSim. También proporciona entorno tipo sandbox para diseccionar software potencialmente maliciosos sin comprometer el sistema primario.

## Análisis de Archivos

En este caso, vamos a ver `oledump.py` para conducir análisis estático en un documento potencialmente malicioso Excel.

`oledump.py` es una herramienta de Python que analiza archivos OLE2, comúnmente llamadas Structured Storage or Compound File Binary Format. OLE significa Object Linking and Embedding, una tecnología propietaria desarrollada por Microsoft. Los archivos OLE2 típicamente solían guardar múltiples tipos de datos, como documentos, hojas de cálculo, presentaciones, dentro de un archivo. Esta herramienta es útil para extraer y examinar los contenidos de los archivos OLE2, conviertiéndolo en un recurso valioso para análisis forense y detección de malware.

