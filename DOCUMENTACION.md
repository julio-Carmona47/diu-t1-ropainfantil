# Documentación de la interfaz — babytool

## 1. Justificación del diseño

### 1.1 Importancia del diseño centrado en el usuario

El diseño centrado en el usuario (DCU) sitúa a la persona que va a usar la aplicación en el centro de todas las decisiones de diseño. En una app de compra de ropa infantil, esto es especialmente crítico porque el usuario suele ir con prisa, compra desde el móvil con una sola mano y, en muchos casos, no tiene al niño delante para probarle la talla. Un mal diseño provoca carritos abandonados, devoluciones costosas y desconfianza en la marca. Aplicar DCU permite reducir la fricción en el flujo de compra, facilitar la elección de talla y transmitir confianza a un público que no es nativo digital. Siguiendo a Norman (2013), un buen diseño debe hacer que las cosas funcionen sin que el usuario tenga que pensar cómo funcionan.

### 1.2 Objetivos y metas del proyecto

Los objetivos del proyecto son medibles y verificables:

1. **Completar una compra en menos de 2 minutos** desde la pantalla de inicio, incluyendo elección de talla y pago.
2. **Reducir la duda de talla:** al menos el 70 % de los usuarios de prueba deben encontrar la guía de tallas sin ayuda en menos de 15 segundos.
3. **Facilitar el uso a una mano:** todas las acciones críticas (buscar, añadir al carrito, pagar) deben estar alcanzables con el pulgar en una pantalla de 360×800 dp.
4. **Cumplir accesibilidad WCAG AA:** todo el texto debe superar un contraste mínimo de 4,5:1 y todas las áreas táctiles deben medir al menos 48×48 dp.

### 1.3 Beneficios esperados

**Para el usuario:** menos tiempo de compra, menos errores de talla, sensación de control con el carrito (con opción de deshacer) y una experiencia accesible para abuelos o personas con poca destreza digital.

**Para el negocio:** mayor tasa de conversión, menos carritos abandonados, menos devoluciones por talla incorrecta, mayor fidelización gracias a la sección de favoritos y datos de comportamiento útiles para futuras campañas.

## 2. Investigación y análisis de usuarios

### 2.1 Datos demográficos y segmentación

El público objetivo son principalmente **madres y padres de 30 a 45 años** que compran ropa para sus hijos de 0 a 14 años, y **abuelos de 55 a 70 años** que compran regalos puntuales. También hay un segmento minoritario de **personas que compran para sobrinos o amigos** (regalos). El dispositivo dominante es el móvil Android, y el contexto de uso habitual es "de pie, con una mano, en ratos muertos" (transporte, sala de espera, sofá).

Se segmenta en:

- **Compradores recurrentes:** madres/padres que compran cada temporada. Valoran rapidez y filtros por talla.
- **Compradores ocasionales:** abuelos o regaladores. Valoran guía de tallas y descripciones claras.
- **Exploradores:** usuarios que miran novedades sin intención inmediata de compra. Valoran favoritos y categorías por edad.

### 2.2 Personas

#### Persona 1: Marta, 38 años, madre de dos hijos (4 y 8 años)

- **Contexto:** Trabaja a jornada completa, compra ropa infantil desde el móvil en el autobús o mientras espera a los niños en extraescolares. Usa una mano.
- **Objetivos:** renovar el armario de los niños sin perder tiempo, encontrar la talla correcta a la primera, aprovechar ofertas.
- **Frustraciones:** webs lentas, no poder filtrar por edad y talla a la vez, no saber si la talla 4 años le quedará al pequeño, y tener que rehacer el carrito si se equivoca.
- **Frase:** "No tengo tiempo para buscar. Si en 30 segundos no encuentro lo que quiero, me voy."

#### Persona 2: Antonio, 67 años, abuelo que compra un regalo a su nieta

- **Contexto:** Compra desde el móvil en casa, con gafas, letra grande. No está acostumbrado a apps de moda. Quiere acertar con la talla porque no vive cerca de la nieta.
- **Objetivos:** comprar un regalo bonito sin equivocarse de talla, pagar de forma segura y que llegue a tiempo.
- **Frustraciones:** letra pequeña, iconos sin texto, formularios largos, no saber qué talla equivale a los años de la niña, y miedo a pagar mal.
- **Frase:** "Solo quiero un pijama talla 4 años. No entiendo por qué es tan complicado."

### 2.3 Análisis de la competencia

| App | Qué hace bien | Qué hace mal | Qué me llevo |
|---|---|---|---|
| **Zara** | Diseño limpio, navegación rápida, imágenes grandes. | No tiene filtro claro por edad/talla infantil; guía de tallas poco accesible en el flujo de compra. | Grid de productos limpio y tipografía clara. |
| **H&M** | Filtros por talla y color muy completos; buena guía de tallas. | Flujo de checkout con demasiados pasos; app pesada. | La guía de tallas accesible como bottom sheet desde el detalle. |
| **Prénatal** | Categorización por edad muy visible (Bebé, Niña, Niño); enfoque claro en padres. | Estética anticuada; iconografía poco clara; poca personalización. | Categorización por edad en la pantalla de inicio. |
| **Vinted** | Excelente sistema de favoritos y notificaciones; filtros potentes. | No es una tienda oficial; no aplica a ropa nueva. | Sección de favoritos como tercer destino de navegación. |

### 2.4 Insights y hallazgos clave

1. **Los usuarios dudan con las tallas.** La equivalencia entre edad y talla varía por marca.
   → **Decisión de diseño:** botón "Guía de tallas" visible en el detalle, que abre un *bottom sheet* con tabla de equivalencias y consejos.

2. **El pulgar manda.** La mayoría usa el móvil con una sola mano y el pulgar no llega a la esquina superior.
   → **Decisión de diseño:** colocar acciones críticas (añadir al carrito, pagar) en la zona inferior de la pantalla, dentro del alcance del pulgar (patrón *thumb zone*).

3. **Equivocarse da miedo.** Eliminar un producto del carrito sin querer genera frustración.
   → **Decisión de diseño:** al eliminar, mostrar un *snackbar* con acción "Deshacer" durante 5 segundos.

4. **El error asusta.** Un formulario de pago con campos mal validados genera abandono.
   → **Decisión de diseño:** usar *text fields* M3 con estado de error claro, mensaje de ayuda y validación en el momento (no solo al enviar).

5. **Los abuelos necesitan letra grande y texto en iconos.**
   → **Decisión de diseño:** tipografía base 16 sp, etiquetas visibles bajo los iconos de la *navigation bar* y áreas táctiles de 48×48 dp como mínimo.

   > **Conclusión de la investigación:** los cinco insights anteriores guían todas las decisiones de diseño que se documentan a partir de la sección 3. Cualquier pantalla del prototipo debe poder justificarse desde al menos uno de ellos.

## 3. Diseño de la interfaz
### 3.1 Mapa de navegación
### 3.2 Wireframes
Wireframes de baja fidelidad en escala de grises, en frames Android Compact de 360×800 dp.

![Wireframe Inicio](capturas/wireframes/01-inicio.png)
![Wireframe Catálogo](capturas/wireframes/02-catalogo.png)
![Wireframe Detalle](capturas/wireframes/03-detalle.png)
![Wireframe Carrito](capturas/wireframes/04-carrito.png)
![Wireframe Checkout](capturas/wireframes/05-checkout.png)
![Wireframe Confirmación](capturas/wireframes/06-confirmacion.png)
![Wireframe Favoritos](capturas/wireframes/07-favoritos.png)
### 3.3 Guía de estilo Material Design 3
### 3.4 Prototipo de alta fidelidad
Prototipo navegable en Figma (enlace en el README). Capturas de las 7 pantallas principales:

![Inicio HD](capturas/prototipo/01-inicio-hd.png)
![Catálogo HD](capturas/prototipo/02-catalogo-hd.png)
![Detalle HD](capturas/prototipo/03-detalle-hd.png)
![Carrito HD](capturas/prototipo/04-carrito-hd.png)
![Checkout HD](capturas/prototipo/05-checkout-hd.png)
![Confirmación HD](capturas/prototipo/06-confirmacion-hd.png)
![Favoritos HD](capturas/prototipo/07-favoritos-hd.png)

## 4. Validación y pruebas
### 4.1 Metodología
### 4.2 Resultados
### 4.3 Iteraciones y mejoras

## 5. Entrega y documentación final
### 5.1 Justificación del diseño propuesto
### 5.2 Recomendaciones y pasos a seguir

## 6. Referencias bibliográficas

Palabra del día: 29