
Es muy importante obtener la fecha de vencimiento de los certificados p12, para poder enviar notificaciones a los clientes para su renovacion, poder enviar recordatorios 30, 15, 7 , 3  y 1 dia antes por ejemplo y asi evitar interrupciones en la facturacion por motivos de vencimiento del certificado.

Tambien poder detectar la fecha de vencimiento de forma automatica para no tener que digitarla manualmente y evitar errores  de digitacion, etc.

# Funciones para obtener la fecha de vencimiento (en PHP pero puedes llevar esta logica a cualquier otro lenguaje de programacion):

### URL codigo en github: 

https://raw.githubusercontent.com/developernsm/fecha_vencimiento_p12/refs/heads/main/fecha_vencimiento_certificado.php

# Uso:

$certP12Path = 'certificado.p12";
$certPassword = 'clave123';
   
$resultado = validarVencimiento($certP12Path, $certPassword);
   
# Resultado:
   
JSON:
   
{
   "valido_desde": "2025-11-25 14:49:00",
   "valido_hasta": "2026-11-25 14:49:00",
   "expirado": false,
   "dias_restantes": 282
}
   

PHP ARRAY:
   
array(4) {
  ["valido_desde"]=> string(19) "2025-11-25 14:49:00"
  ["valido_hasta"]=> string(19) "2026-11-25 14:49:00"
  ["expirado"]=> bool(false)
  ["dias_restantes"]=> float(282)
}
