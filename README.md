# API CONSULTAR TRACKID DTE SII

## DESCRIPCIÓN:

La <b>API Consultar TrackID DTE</b> esta diseñada para que el programador pueda realizar una fácil y rápida Integración con Sistema Propio. El objetivo de esta api es <b>"Obtener el estado de los Documentos enviados al sii"</b>.
<br>La comunicación entre el Servidor y Cliente se realiza a traves de Datos Json o archivos txt.
 
## PRECIOS:

La <b>API Consultar TrackID DTE</b>, se encuentra disponible en 2 modalidades; Pago Único y Pago Mensual.
<br>En ambos casos el método de integración es el mismo, lo que cambia solo es la url del endpoint de la api.
<br>Esto quiere decir que si contrata la modalidad pago mensual y posteriormente quiere compra la api, 
solo deberá cambiar la url a la cual envía el json o archivo txt.
<br>
<br>Precio Modalidad Pago Único: <b>4 UF</b> $148.000.- Aprox. (Descuento)
<br>-Se utiliza en servidores propios del cliente
<br>-Sin limite de Consultas.
<br>
<br>Precio Modalidad Pago Mensual: <b>1 UF = $37.000</b>.- aprox.
<br>-Se utiliza en servidores de Factronica
<br>-Limite de 60 consultas por minuto.
<br>-
<br>(Descuento) Los clientes que ya han comprado la API factura electrónica o boleta electrónica, tienen un <b>50% de descuento</b> en la modalidad pago único.
<br>
## CARACTERÍSTICAS:

![](https://scanapp.org/assets/github_assets/done.png) **Compatibilidad:** Windows, Linux, Mac, Android y Iphone.

![](https://scanapp.org/assets/github_assets/done.png) **Integración:** ApiRest Datos Json o Archivo Txt

![](https://scanapp.org/assets/github_assets/done.png) **Código Abierto:** Al comprar la Api se entrega código fuente.

![](https://scanapp.org/assets/github_assets/done.png) **Acceso SII Chile:** Acceso al SII con Certificado Digital.
 
## PASOS A SEGUIR PARA LA INTEGRACIÓN:

A continuación se detalla el procedimiento a realizar en la integración.

-   Paso 01.-Crear datos json o archivo txt
-   Paso 02.-Enviar datos Json o archivo txt
-   Paso 03.-Procesar Respuesta Json o archivo txt

## PASO 01:
Crear archivo txt o datos json con los datos requeridos de acuerdo a los siguientes ejemplos:

## FORMATO JSON:
````
{
	"Token": "qwerty",
	"RutEmisor": "11111111-1",
	"TrackId": "4506206192",
	"Modulus": "nnn",
	"Exponent": "nnn",
	"X509Certificate": "nnn",
	"PrivKey": "nnn"
}
````

## FORMATO TXT:
````
<?php
$FACTRONICA["RutCompania"]="11111111"; 
$FACTRONICA["DvCompania"]="1"; 
$FACTRONICA["TrackId"]="4506206192";
$FACTRONICA["Modulus"]="nnn"; 
$FACTRONICA["Exponent"]="nnn"; 
$FACTRONICA["X509Certificate"]="nnn";
$FACTRONICA["PrivKey"]="nnn";
$FACTRONICA["RESPUESTASII"]="RUT765468108_TIPO61_FOLIO800_RESPUESTAENVIODTE.xml";
$FACTRONICA["BUZONRESPUESTAS"]="temp_respuestas";
?>
````

## PASO 02: ENVIAR PETICIÓN A LA API

Enviar la petición con el txt o datos json a la url endpoint del servidor. 

## ENVIAR JSON CON CURL
````
curl -X POST --header 'Content-Type: application/json' -d '{"Token": "qwerty","RutEmisor": "11111111-1","TrackId": "4506206192","Modulus": "nnn","Exponent": "nnn","X509Certificate": "nnn","PrivKey": "nnn"}' https://www.suhost.cl/api/factronica_factura_consultartrackid/index.php
````

## ENVIAR TXT CON CURL
````
curl --form "Token=qwerty" --form "archivotxt=@dte.php" https://www.suhost.cl/api/factronica_factura_consultartrackid/index.php
````

## PASO 03: RECUPERAR RESPUESTA DE LA API
	
La respuesta que entrega la api es en formato json. 

<br>Ejemplo respuesta json:
````
{
	"api":
	{
		"Codigo":"220",
		"Estado":"OK",
		"Mensaje":"Respuesta recibida correctamente"
	},
	"sii":
	{
		"SIIRESP_BODY":
		{
			"TIPO_DOCTO":"61",
			"INFORMADOS":"1",
			"ACEPTADOS":"1",
			"RECHAZADOS":"0",
			"REPAROS":"0"
		},
		"SIIRESP_HDR":
		{
			"TRACKID":"8234892492",
			"ESTADO":"EPR",
			"GLOSA":"Envio Procesado",
			"NUM_ATENCION":"718689   ( 2024\/03\/31 13:17:31)"
		}
	}
}
````

<br>Ejemplo respuesta en php:
````
<?php 
 $respuesta_sii = [
   "api" => [
         "Codigo" => "220", 
         "Estado" => "OK", 
         "Mensaje" => "Respuesta recibida correctamente" 
      ], 
   "sii" => [
            "SIIRESP_BODY" => [
               "TIPO_DOCTO" => "61", 
               "INFORMADOS" => "1", 
               "ACEPTADOS" => "1", 
               "RECHAZADOS" => "0", 
               "REPAROS" => "0" 
            ], 
            "SIIRESP_HDR" => [
                  "TRACKID" => "8234892492", 
                  "ESTADO" => "EPR", 
                  "GLOSA" => "Envio Procesado", 
                  "NUM_ATENCION" => "718689   ( 2024/03/31 13:17:31)" 
               ] 
         ] 
]; 
````
