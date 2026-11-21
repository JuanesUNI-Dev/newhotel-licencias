# Licencias - NewHotel POS

Un archivo JSON por cliente en `lic/<cliente>.json`. El POS lo consulta al arrancar.

```json
{ "cliente": "lf-7f3c9a2b", "activo": true, "expira": "2027-11-21", "sig": "<hmac>" }
```

* `activo: false` -> el POS bloquea (suscripcion suspendida).
* `expira` en el pasado -> bloquea (suscripcion vencida).
* La firma es HMAC-SHA256 de `cliente|activo|expira` con el secreto del proveedor;
  sin ella no se puede inventar una licencia.

## Renovar

```
powershell -File <repo-POS>\tools\licencia\generar_licencia.ps1 -Cliente lf-7f3c9a2b -Expira 2028-11-21 -OutDir lic
```

y subir el archivo (reemplaza al anterior).

## Suspender

```
... -Suspender
```

## Importante

El POS lee los archivos por `raw.githubusercontent.com` **sin autenticacion**: el repositorio
debe ser **publico**. No contiene datos de clientes ni secretos, solo ids aleatorios, fechas y firmas.
El secreto de firma vive unicamente en el equipo del proveedor.