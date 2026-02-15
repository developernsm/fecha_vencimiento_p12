# fecha_vencimiento_p12

# Funcion para obtener Vecha de vencimiento de los Certificados de firma digital (en PHP pero puedes llevar esta logica a cualquier lenguaje de programacion)

  function verificarCertificado($rutaP12, $password)
  {
        if (!file_exists($rutaP12)) {
            throw new \Exception("Certificado no encontrado.");
        }

        $contenido = file_get_contents($rutaP12);

        if (!openssl_pkcs12_read($contenido, $certs, $password)) {
            throw new \Exception("No se pudo leer el certificado. Verifique la contraseña.");
        }

        $certificado = $certs['cert'];

        $info = openssl_x509_parse($certificado);

        return $info;
   }

  function validarVencimiento($rutaP12, $password)
   {
        $info = $this->verificarCertificado($rutaP12, $password);

        $fechaInicio = $info['validFrom_time_t'];
        $fechaFin = $info['validTo_time_t'];

        $ahora = time();

        $expirado = $ahora > $fechaFin;

        $diasRestantes = floor(($fechaFin - $ahora) / 86400);

        return [
            'valido_desde' => date('Y-m-d H:i:s', $fechaInicio),
            'valido_hasta' => date('Y-m-d H:i:s', $fechaFin),
            'expirado' => $expirado,
            'dias_restantes' => $diasRestantes
        ];
   }
   
   # Uso:
   
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

