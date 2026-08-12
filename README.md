# Bifrost

Proxy de tickets para aplicaciones desplegadas en el mismo CapRover.

Una peticion publica como:

```text
https://bifrost.maytok.com/empresa-ejemplo/123e4567-e89b-12d3-a456-426614174000
```

se envia internamente a:

```text
http://srv-captain--encomiendas-empresa-ejemplo/courier/pdf-ticket/80mm/123e4567-e89b-12d3-a456-426614174000
```

## Agregar empresas

Agrega una linea al bloque `map` de `default.conf` por cada empresa:

```nginx
map $uri $company_upstream {
    default "";
    ~^/empresa-ejemplo/ srv-captain--encomiendas-empresa-ejemplo;
    ~^/otra-empresa/   srv-captain--encomiendas-otra-empresa;
}
```

Los nombres no incluidos responden con `404`.

## Despliegue en CapRover

1. Crea una aplicacion llamada `bifrost`.
2. Despliega este repositorio mediante el metodo que prefieras (CLI, GitHub o tarball).
3. Asocia `bifrost.maytok.com` a la aplicacion y activa HTTPS.

No necesitas publicar puertos adicionales ni configurar `UPSTREAM_HTTP_ADDRESS`.
