# BasicMarket

**Aplicación móvil para la venta de productos básicos de primera necesidad**

## Descripción
BasicMarket permite consultar productos, armar un carrito, realizar pedidos y pagar mediante PayPhone, transferencia bancaria o efectivo al recibir/retirar, según las condiciones configuradas por la tienda. También integra las ventas presenciales para compartir el inventario y los reportes.

## Objetivo
Facilitar la compra de productos básicos y apoyar a una tienda en la administración de catálogo, inventario, pedidos, pagos, caja, notificaciones y reportes desde un sistema integrado.

## Usuarios del sistema
| Rol | Responsabilidades |
|---|---|
| Cliente | Consultar el catálogo, administrar el carrito, realizar pedidos y pagos, revisar el historial, favoritos y notificaciones. También puede comprar en tienda con o sin cuenta. |
| Cajero | Registrar ventas presenciales, cobrar, entregar pedidos retirados en tienda y abrir/cerrar su caja. No puede cambiar precios ni gestionar usuarios. |
| Repartidor | Consultar solo las entregas asignadas, marcar pedidos como entregados y registrar el cobro en efectivo cuando corresponda. |
| Administrador | Gestionar productos, inventario, pedidos, pagos, transferencias, reembolsos, cajas, usuarios, configuración y reportes. |

## Módulos principales
1. Autenticación.
2. Catálogo de productos.
3. Carrito de compras.
4. Pedidos.
5. Pagos.
6. Notificaciones.
7. Inventario.
8. Administración.
9. Venta en tienda.
10. Reportes.

## Arquitectura
- Arquitectura Cliente-Servidor con microservicios.
- Aplicación móvil Android desarrollada con Flutter y Dart.
- Backend con Node.js y Express.js.
- API REST y API Gateway como punto de entrada de la aplicación.
- Seis servicios: Autenticación; Catálogo e Inventario; Pedidos; Pagos; Notificaciones; Reportes.
- MySQL con una base de datos por servicio.
- Arquitectura hexagonal en Pagos y Notificaciones para aislar integraciones externas.
- DDD aplicado de forma ligera para delimitar responsabilidades.

## Tecnologías e integraciones
| Tecnología | Uso |
|---|---|
| Flutter y Dart | Aplicación móvil |
| Node.js y Express.js | Backend y servicios REST |
| MySQL | Persistencia de datos |
| JWT y bcrypt | Sesiones y protección de contraseñas |
| flutter_secure_storage | Almacenamiento seguro del token en el dispositivo |
| PayPhone | Pago con tarjeta |
| Nodemailer con Gmail SMTP o Resend | Correo electrónico |
| API de Meta WhatsApp | Mensajes mediante plantillas aprobadas |
| Firebase Cloud Messaging | Notificaciones dentro de la app (opcional) |
| Jest, Supertest, flutter_test y Postman | Pruebas |
| Docker Compose y GitHub Actions | Contenedores e integración continua |
| Sentry | Monitoreo de errores |

## Métodos de pago
- **Tarjeta:** mediante PayPhone. BasicMarket no almacena datos de tarjeta y el servidor confirma el resultado consultando a PayPhone.
- **Transferencia:** el pedido genera una referencia única; el cliente adjunta el comprobante y el administrador lo valida manualmente.
- **Efectivo:** al recibir o retirar el pedido, sujeto a límites y condiciones definidos por la tienda.

## Reglas de negocio importantes
- Reserva de inventario: 15 minutos para tarjeta y 24 horas para transferencia.
- Cada intento de pago debe tener una clave única para evitar cobros duplicados.
- El servidor confirma los pagos; no se confía únicamente en la respuesta de la aplicación.
- Los estados del pedido son: Pendiente de pago, Pagado, En preparación, Entregado, Cancelado, Pago rechazado, Expirado y Reembolsado.
- Los cambios de precio no modifican pedidos confirmados.
- WhatsApp requiere consentimiento expreso; el correo sirve como canal de respaldo.
- Las ventas en línea y presenciales comparten el inventario.

## Alcance y limitaciones de la primera versión
- Una sola tienda.
- Android inicialmente.
- Requiere conexión a Internet.
- El costo de envío es fijo y lo define la tienda; no se calcula por distancia.
- No incluye geolocalización, seguimiento de entrega en mapa ni chat en tiempo real.
- La facturación electrónica con el SRI queda para una fase posterior.

## Instalación y ejecución
El documento original define las tecnologías y la arquitectura, pero no especifica todavía la estructura real del repositorio, las carpetas, los puertos, los comandos de ejecución ni las variables de entorno definitivas. Por eso, no se incluyen comandos supuestos.

Cuando esté disponible el repositorio de código:
1. Revisar y documentar la estructura real de Flutter y de los seis servicios backend.
2. Registrar las versiones de Flutter, Dart, Node.js y MySQL utilizadas.
3. Crear archivos `.env.example` con nombres de variables y valores ficticios; nunca incluir claves reales.
4. Documentar los comandos reales para instalar dependencias, ejecutar pruebas y levantar cada servicio.
5. Mantener separados los entornos de desarrollo, pruebas y producción.
6. Configurar PayPhone, correo y WhatsApp con credenciales de prueba antes de utilizar cuentas reales.

## Pruebas
El plan original contempla:
- Pruebas unitarias con Jest y `flutter_test`.
- Pruebas de integración con Jest y Supertest.
- Pruebas de API con Postman.
- Pruebas de pago en el entorno de PayPhone.
- Pruebas de seguridad, concurrencia, usabilidad y dispositivos Android.

## Documentos relacionados
- `DERCAS_BasicMarket.docx`: documento de especificación del proyecto, con alcance, requisitos, reglas, arquitectura, criterios, pruebas y riesgos.
- `AGENTS.md`: instrucciones para el agente de inteligencia artificial que trabaje en el código del proyecto.
- `README.md`: presentación y guía general del proyecto.

## Estado del proyecto
Esta documentación se preparó tomando como base el documento original de BasicMarket. Los detalles concretos del repositorio, credenciales, configuración y comandos de ejecución deberán completarse cuando exista o se comparta el código fuente.

## Datos académicos
- Escuela Superior Politécnica Agropecuaria de Manabí “Manuel Félix López”.
- Carrera de Computación.
- Asignatura: Desarrollo de Aplicaciones para Dispositivos Móviles.
- Autor: Héctor Javier Sandoval de la Cruz.
- Facilitador: Ing. Alfonso Tomás Loor Vera.
- Documento base: octubre de 2026.
