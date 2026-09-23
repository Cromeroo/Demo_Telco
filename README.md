# Demo Telco — Nestlé B2B · Pedidos en vivo

Pantalla minimalista en vivo para demo B2B de telemercadeo Nestlé (resurtido de tiendas).
Muestra la ficha del cliente y el carrito en tiempo real desde Firebase Realtime Database.

## Estructura

| Archivo | Descripción |
|---|---|
| `index.html` | Pantalla principal (light corporativo, escucha `/pedidos`, selector de historial, totales en vivo) |
| `dashboard-dark.html` | Variante anterior modo oscuro (respaldo) |
| `flujo_bot_procesos.drawio` | Diagrama BPMN del flujo del bot (abrir en app.diagrams.net) |

## Uso

```bash
# servir local
python -m http.server 3000
# abrir http://localhost:3000
```

O simplemente doble clic en `index.html` (requiere internet para el SDK de Firebase).

## Datos (Firebase RTDB)

- URL: `https://demotest-4c241-default-rtdb.firebaseio.com`
- Nodo: `/pedidos` — cada hijo es un pedido `{ cliente: { nombre, tienda }, items: { ... } }`.
- La pantalla sigue automáticamente al pedido actualizado más recientemente; el dropdown permite ver el historial.
- Nodos con solo `cliente` + nodos con solo `items` e ID relacionado (`PED-NOMBRE-###`) se fusionan por coincidencia de nombre.

## Probar

```bash
# sembrar un pedido de ejemplo
curl -X PUT https://demotest-4c241-default-rtdb.firebaseio.com/pedidos/PED-EJEMPLO-001.json \
  -H "Content-Type: application/json" \
  -d '{"cliente":{"nombre":"Demo","tienda":"Tienda Demo"},"items":{"i1":{"nombre":"Nescafé Clásico 200 g","cantidad":1,"precio_unitario":2450,"subtotal":2450}}}'
```
