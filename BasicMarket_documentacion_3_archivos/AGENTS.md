# AGENTS.md --- Instrucciones para trabajar en BasicMarket

## 1. Propósito del archivo

Este archivo contiene instrucciones para un agente de programación (por
ejemplo, un asistente de código) que ayude a desarrollar BasicMarket. No
reemplaza el documento de requisitos/DERCAS: lo complementa indicando
cómo debe trabajar el agente dentro del repositorio.

## 2. Contexto del proyecto

BasicMarket es una aplicación móvil Android para vender productos
básicos de primera necesidad. Los usuarios son cliente, cajero,
repartidor y administrador. La aplicación móvil se plantea con
Flutter/Dart; el backend con Node.js/Express; la persistencia con MySQL;
y la comunicación mediante API REST y un API Gateway.

Para el desarrollo de esta aplicacion tome como referencia el contexto de este archivo
[DERCAS_BasicMarket.docx](./DERCAS_BasicMarket.docx)


## 3. Arquitectura acordada

-   Mantener el enfoque cliente-servidor con microservicios descrito en
    la especificación.
-   Considerar estos servicios: Autenticación; Catálogo e Inventario;
    Pedidos; Pagos; Notificaciones; Reportes.
-   La app móvil se comunica con el API Gateway; no debe conectarse
    directamente a las bases de datos.
-   Mantener las integraciones externas aisladas: PayPhone en Pagos;
    correo y WhatsApp en Notificaciones.
-   No introducir una arquitectura distinta ni nuevas tecnologías
    principales sin justificarlo y solicitar aprobación.

## 4. Reglas funcionales y de negocio que no se deben romper

-   Los roles son cliente, cajero, repartidor y administrador; aplicar
    permisos según el rol.
-   El inventario de ventas en línea y presenciales es compartido.
-   Validar stock y precio en el servidor antes de confirmar una compra.
-   El servidor, no la app móvil, confirma el resultado del pago
    consultando a PayPhone.
-   No almacenar números ni datos sensibles de tarjetas.
-   Cada intento de pago debe tener una clave única/idempotente para
    evitar cobros duplicados.
-   Las transferencias requieren revisión del comprobante por el
    administrador.
-   Registrar auditoría para cambios importantes de pagos, inventario,
    usuarios, pedidos y caja.
-   No permitir que cajeros cambien precios o administren usuarios.
-   El repartidor solo puede consultar los pedidos que le han sido
    asignados.
-   Respetar los estados y transiciones de pedido definidos en el
    documento de requisitos.

## 5. Seguridad y privacidad

-   Nunca escribir contraseñas, tokens, claves API, credenciales o datos
    bancarios reales en el código, pruebas, documentación pública o
    logs.
-   Utilizar variables de entorno y mantener los archivos `.env` fuera
    del control de versiones.
-   Almacenar contraseñas mediante un algoritmo de hash apropiado (el
    proyecto especifica bcrypt).
-   Validar los datos tanto en el cliente como en el servidor; la
    validación del servidor es obligatoria.
-   Aplicar autorización en cada endpoint, no solamente ocultando
    botones en la interfaz.
-   No registrar tokens, contraseñas ni datos de tarjetas en logs.
-   Usar HTTPS en entornos desplegados.
-   Tratar los datos personales conforme a la normativa ecuatoriana
    aplicable.

## 6. Forma de trabajo del agente

1.  Antes de modificar código, revisar la estructura y los archivos
    existentes.
2.  Leer el documento de requisitos y localizar el módulo afectado.
3.  Explicar brevemente qué archivos piensa modificar y por qué.
4.  Implementar cambios pequeños y coherentes con la arquitectura
    existente.
5.  No inventar requisitos, reglas comerciales, endpoints, tablas ni
    credenciales.
6.  Si falta una decisión importante, preguntar antes de asumirla.
7.  No eliminar ni sobrescribir trabajo existente sin autorización.
8.  Mantener nombres, convenciones y estilo de código ya utilizados en
    el repositorio.
9.  Actualizar documentación cuando cambie un comportamiento o contrato
    de API.

## 7. Pruebas y calidad

-   Añadir o actualizar pruebas para cada comportamiento nuevo o
    corregido.
-   Probar casos correctos, datos inválidos, permisos insuficientes y
    errores de servicios externos.
-   Para backend, utilizar las herramientas de pruebas definidas por el
    proyecto (Jest/Supertest).
-   Para Flutter, utilizar `flutter_test`.
-   No afirmar que una función está terminada si no se ejecutaron las
    pruebas pertinentes.
-   Informar qué pruebas se ejecutaron, cuáles pasaron y cuáles no
    pudieron ejecutarse.

## 8. Criterios para considerar una tarea terminada

Una tarea se considera terminada cuando: - Cumple el requisito asociado
y sus criterios de aceptación. - Respeta roles, seguridad y reglas de
negocio. - Incluye pruebas pertinentes. - No introduce errores conocidos
en otras funciones. - La documentación relacionada queda actualizada. -
Se informa cualquier limitación o pendiente.

## 9. Límites de actuación

-   No realizar pagos reales ni usar cuentas de producción durante
    pruebas.
-   No enviar mensajes reales a clientes sin autorización explícita.
-   No desplegar a producción, borrar datos, ejecutar migraciones
    destructivas ni cambiar credenciales sin aprobación humana.
-   No aprobar transferencias, reembolsos o anulaciones reales de manera
    autónoma.
-   Para operaciones financieras o irreversibles, detenerse y solicitar
    confirmación humana.

## 10. Formato de respuesta del agente

Al finalizar cada tarea, informar: - Resumen de lo realizado. - Archivos
creados o modificados. - Requisitos relacionados. - Pruebas ejecutadas y
resultados. - Riesgos, supuestos y tareas pendientes.

Despues de finalizar y aprobada una tarea realiza un commit.
Git add:
Git commit -m "descripcion de la tarea"
Git push
los repositorios son:
Backend:
Frontend:
AdminWeb: