# Mkdir-HormigasAIS-Open-Lab-
Un espacio donde desarrolladores, diseñadores y creadores puedan colaborar en proyectos de automatización de marketing, scraping de datos, análisis SEO y desarrollo de contenido con IA.

<<https://www.linkedin.com/newsletters/hormigasais-community-7307138608543490048
# QR Decoder - ZXing Integration

Este módulo forma parte del laboratorio abierto **HormigasAIS Open Lab** y tiene como objetivo demostrar cómo utilizar la librería [ZXing](https://github.com/zxing/zxing) para decodificar códigos QR de forma eficiente.

## ¿Qué es ZXing?

ZXing (Zebra Crossing) es una librería open source para leer y generar códigos de barras 1D y 2D, ampliamente utilizada en aplicaciones móviles, web y de escritorio. Esta integración se enfoca en decodificación visual de códigos QR para propósitos de autenticación, scraping y automatización de procesos.

## Estructura


## Requisitos

- [ZXing Java SE](https://github.com/zxing/zxing)
- Java instalado
- Python 3.x
- Librería `jpype` (puente entre Python y Java)

## Licencia

Este módulo está inspirado en [ZXing](https://github.com/zxing/zxing), bajo licencia Apache-2.0. Ver [REUSE](https://reuse.software/) para más detalles sobre metadatos y derechos de autor.

---
Creado con la mente curiosa y el corazón dispuesto por [HormigasAIS](https://github.com/HormigasAIS).
import jpype
import jpype.imports
from jpype.types import *

# Ruta al ZXing core .jar (descárgalo desde GitHub Releases)
ZXING_PATH = "zxing-core-3.5.3.jar"

if not jpype.isJVMStarted():
    jpype.startJVM(classpath=[ZXING_PATH])

from com.google.zxing import BinaryBitmap
from com.google.zxing.common import HybridBinarizer
from com.google.zxing import MultiFormatReader
from com.google.zxing.client.j2se import BufferedImageLuminanceSource
from javax.imageio import ImageIO
from java.io import File

def decode_qr(image_path):
    image = ImageIO.read(File(image_path))
    source = BufferedImageLuminanceSource(image)
    bitmap = BinaryBitmap(HybridBinarizer(source))
    result = MultiFormatReader().decode(bitmap)
    print("Resultado del QR:", result.getText())

decode_qr("sample-qr.png")
