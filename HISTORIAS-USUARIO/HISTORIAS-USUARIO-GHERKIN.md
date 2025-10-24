## Ejemplo 1

Historia de usuario (BDD)

Como Coordinador
Quiero poder asignar entregas a repartidores
Para distribuir eficientemente las guías y garantizar que las entregas se realicen correctamente.

### Criterios de aceptación

El sistema debe permitir asignar guías de forma manual a repartidores disponibles.

El sistema debe sugerir repartidores automáticamente según zona, cercanía o carga laboral.

El sistema debe registrar la asignación realizada para que quede constancia.

El repartidor debe poder ver las entregas asignadas en su aplicación.

### Escenarios en Gherkin

Feature: Gestión de entregas
  Como coordinador
  Quiero asignar entregas a repartidores
  Para distribuir eficientemente las guías

  Scenario: Asignación manual de entrega a repartidor

    Given que soy coordinador
    And hay repartidores disponibles
    When creo una nueva entrega
    And asigno manualmente un repartidor
    Then el sistema debe registrar la asignación realizada
    And el repartidor debe ver la entrega en su aplicación

  Scenario: Sugerencia automática de repartidor

    Dado que soy coordinador
    Y hay entregas sin asignar
    Cuando reviso las entregas pendientes
    Entonces el sistema debe sugerir repartidores según zona, cercanía o carga laboral

## Ejemplo 2

Historia de usuario (BDD)

Como Administrador de catálogo
Quiero registrar un nuevo producto
Para que esté disponible en la tienda y pueda ser vendido.

### Criterios de aceptación

El formulario debe permitir SKU, nombre, descripción, categoría, precio, impuestos y stock inicial.

Validar que el SKU sea único.

Permitir subir hasta 5 imágenes con tamaño y formato aceptados.

El producto debe quedar en estado "Publicado" o "Borrador" según elección.

### Escenarios en Gherkin

Feature: Registro de producto
  Como administrador de catálogo
  Quiero registrar un nuevo producto
  Para publicarlo en la tienda

  Scenario: Registro exitoso de producto publicado

    Given que tengo permisos de administrador
    When completo todos los campos obligatorios con datos válidos
    And subo imágenes válidas
    Then el producto se crea con SKU único
    And queda en estado "Publicado"

  Scenario: Intento de registro con SKU duplicado

    Given que existe un producto con SKU "ABC123"
    When intento crear otro producto con SKU "ABC123"
    Then el sistema muestra un error indicando SKU duplicado
    And no crea el producto

Ejemplo 3

Historia de usuario (BDD)

Como Usuario
Quiero ver el historial de mis pedidos
Para revisar compras pasadas y descargar recibos.

### Criterios de aceptación

Mostrar lista de pedidos con fecha, estado, total y número de pedido.

Permitir filtrar por rango de fechas y estado.

Permitir ver detalle de pedido y descargar recibo en PDF.

Paginación para muchos pedidos.

### Escenarios en Gherkin

Feature: Visualización de historial de pedidos
  Como usuario
  Quiero ver mi historial de pedidos
  Para revisar compras y descargar recibos

  Scenario: Ver detalle de pedido y descargar recibo

    Given que soy usuario autenticado
    And tengo pedidos anteriores
    When accedo a "Mis pedidos" y abro un pedido
    Then veo el detalle completo y el botón para descargar el recibo en PDF

  Scenario: Filtrar pedidos por fecha

    Given que tengo pedidos en varios meses
    When filtro pedidos entre 2025-01-01 y 2025-03-31
    Then la lista muestra sólo los pedidos en ese rango

## Ejemplo 4

Historia de usuario (BDD)

Como Responsable de seguridad
Quiero gestionar permisos de usuarios (roles y privilegios)
Para controlar el acceso a funcionalidades sensibles.

### Criterios de aceptación

Crear, editar y eliminar roles con permisos asociados.

Asignar uno o varios roles a usuarios.

Validar que cambios de permisos se aplican en tiempo real.

Mantener un log de cambios con usuario responsable y timestamp.

### Escenarios en Gherkin


Feature: Gestión de permisos y roles
  Como responsable de seguridad
  Quiero controlar roles y privilegios
  Para asegurar acceso correcto

  Scenario: Creación de un rol con permisos específicos

    Given que soy administrador con permiso para gestionar roles
    When creo un rol "GestorInventario" con permisos de lectura y escritura en inventario
    Then el rol se crea y aparece en la lista de roles

  Scenario: Asignación de rol a usuario

    Given que existe el rol "GestorInventario"
    And hay un usuario "juan.perez"
    When le asigno el rol a juan.perez
    Then juan.perez recibe los permisos correspondientes inmediatamente

## Ejemplo 5

Historia de usuario (BDD)

Como Operador de almacén
Quiero registrar entradas y salidas de inventario
Para mantener el stock actualizado y auditable.

### Criterios de aceptación

Registrar movimientos: tipo (entrada/salida), SKU, cantidad, motivo y documento asociado.

Validar no permitir salida si stock insuficiente (salvo autorización especial).

Mantener historial de movimientos con filtros por fecha y tipo.

Generar notificaciones si el stock queda por debajo del mínimo.

### Escenarios en Gherkin


Feature: Registro de movimientos de inventario
  Como operador de almacén
  Quiero registrar entradas y salidas
  Para mantener stock actualizado

  Scenario: Registro de entrada de inventario

    Given que recibimos un nuevo lote de producto X
    When registro una entrada de 50 unidades con documento de compra
    Then el stock de producto X aumenta en 50 unidades
    And queda registrado el movimiento con el documento asociado

  Scenario: Bloqueo por salida con stock insuficiente

    Given que el stock de producto Y es 2
    When intento registrar una salida de 5 unidades
    Then el sistema bloquea la operación por stock insuficiente
    And sugiere crear una orden de reposición

## Ejemplo 6

Historia de usuario (BDD)

Como Soporte Técnico
Quiero consultar el historial de actividad de un usuario (logs)
Para investigar incidentes y auditorías.

### Criterios de aceptación

Registrar eventos: inicios de sesión, cambios de configuración y operaciones críticas.

Permitir búsqueda por usuario, tipo de evento y rango de fechas.

Incluir IP, timestamp y resultado (éxito/fallo).

Acceso restringido a roles autorizados.

### Escenarios en Gherkin


Feature: Historial de actividad de usuarios
  Como soporte técnico
  Quiero revisar logs de actividad
  Para investigar incidentes

  Scenario: Búsqueda de intentos de acceso fallidos

    Given que soy auditor con permisos para ver logs
    When busco eventos de tipo "login_failed" para usuario "ana.gomez" entre 2025-06-01 y 2025-06-30
    Then se muestran todos los intentos fallidos con IP y timestamp

  Scenario: Restricción de acceso a logs

    Given que soy un usuario sin rol de auditoría
    When intento acceder al historial de actividad
    Then el sistema deniega el acceso y muestra mensaje de permiso insuficiente

## Ejemplo 7

Historia de usuario (BDD)

Como Gestor de promociones
Quiero crear campañas promocionales con descuentos por periodo
Para aumentar ventas en temporadas específicas.

### Criterios de aceptación

Crear campaña con nombre, fechas, condiciones, tipo de descuento y límite de uso.

Validar que no se solape con otra campaña del mismo tipo.

Aplicar descuento en checkout automáticamente.

Reportar métricas de rendimiento (uso, ahorro generado).

### Escenarios en Gherkin


Feature: Creación de campañas promocionales
  Como gestor de promociones
  Quiero definir descuentos por periodo
  Para incentivar ventas

  Scenario: Campaña válida aplicada en checkout

    Given que existe una campaña del 20% para la categoría "Ropa" vigente hoy
    When un cliente compra un producto de "Ropa" en checkout
    Then el descuento del 20% se aplica automáticamente al total

  Scenario: Prevención de solapamiento de campañas

    Given que hay una campaña activa para SKU "123" del 1 al 10 de julio
    When intento crear otra campaña para el mismo SKU entre el 5 y 15 de julio
    Then el sistema muestra advertencia de solapamiento y evita la creación

# Ejemplo 8

Historia de usuario (BDD)

Como Responsable de calidad
Quiero registrar y gestionar devoluciones y reclamos
Para procesar reembolsos y mejorar procesos.

### Criterios de aceptación

Crear RMA ligado al pedido y motivo.

Validar plazos de devolución según política.

Flujo de inspección: recibido, verificado, aprobado/rechazado.

Notificar al cliente del estado y generar reembolso cuando aplique.

### Escenarios en Gherkin


Feature: Gestión de devoluciones y reclamos
  Como responsable de calidad
  Quiero procesar devoluciones correctamente
  Para gestionar reembolsos y calidad

  Scenario: Creación de RMA dentro del plazo

    Given que el pedido fue entregado hace 5 días y la política permite 30 días
    When el cliente solicita una devolución y se crea RMA
    Then el RMA queda registrado y el cliente recibe instrucciones de envío

  Scenario: Rechazo de devolución por plazo vencido

    Given que el pedido fue entregado hace 45 días y la política permite 30 días
    When el cliente solicita la devolución
    Then el sistema rechaza la solicitud por plazo vencido y notifica al cliente

# Ejemplo 9

Historia de usuario (BDD)

Como Analista
Quiero exportar reportes de ventas por período y categoría
Para analizar rendimiento y tomar decisiones.

### Criterios de aceptación

Generar reportes filtrables por fecha, categoría, canal y vendedor.

Exportar a CSV y PDF.

Programar reportes automáticos (diario, semanal, mensual).

Respetar permisos de acceso a datos.

### Escenarios en Gherkin


Feature: Exportación de reportes de ventas
  Como analista
  Quiero exportar datos de ventas
  Para análisis y toma de decisiones

  Scenario: Exportar reporte mensual a CSV

    Given que tengo permiso para ver ventas
    When genero un reporte de ventas del mes pasado por categoría y lo exporto a CSV
    Then se descarga un archivo CSV con columnas y totales correctos

  Scenario: Programar envío automático de reporte

    Given que estoy configurando un reporte semanal
    When programo el envío para todos los lunes a las 08:00
    Then el sistema envía el reporte automáticamente según programación

## Ejemplo 10

Historia de usuario (BDD)

Como Usuario
Quiero actualizar mi dirección de envío en mi perfil
Para que los pedidos futuros lleguen al lugar correcto.

### Criterios de aceptación

Permitir agregar múltiples direcciones y marcar una como predeterminada.

Validar campos obligatorios.

Usar la dirección predeterminada en checkout por defecto.

Impedir eliminar la única dirección predeterminada.

### Escenarios en Gherkin


Feature: Gestión de direcciones de envío
  Como usuario
  Quiero actualizar mis direcciones
  Para enviar pedidos correctamente

  Scenario: Agregar nueva dirección y marcarla predeterminada

    Given que soy usuario autenticado
    When agrego una nueva dirección válida y la marco como predeterminada
    Then la nueva dirección se guarda y se usa por defecto en checkout

  Scenario: Impedir eliminación de la única dirección predeterminada

    Given que tengo solo una dirección marcada como predeterminada
    When intento eliminarla
    Then el sistema impide la eliminación y solicita añadir otra dirección primero

## Ejemplo 11

Historia de usuario (BDD)

Como Responsable de integraciones
Quiero configurar y probar integraciones con transportistas externos
Para automatizar la generación de guías y el seguimiento.

### Criterios de aceptación

Guardar credenciales y endpoints por transportista de forma segura.

Probar conexión y listar servicios disponibles.

Generar número de guía automáticamente al confirmar envío.

Registrar errores de integración con detalles para soporte.

### Escenarios en Gherkin


Feature: Integración con transportistas
  Como responsable de integraciones
  Quiero conectar con APIs de transporte
  Para automatizar guías y seguimiento

  Scenario: Probar conexión con transportista exitosamente

    Given que tengo credenciales válidas del transportista X
    When ejecuto la prueba de conexión desde la configuración
    Then el sistema muestra "Conexión exitosa" y lista servicios disponibles

  Scenario: Generación automática de guía al confirmar envío
  
    Dado que la orden está lista para envío y la integración está activa
    Cuando confirmo la creación del envío
    Entonces el sistema solicita la guía al transportista y guarda el número de guía en la orden