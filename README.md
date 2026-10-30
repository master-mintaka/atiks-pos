# Atik's POS

**Español** · [English](#english)

Punto de venta muy sencillo para **Atik's Café**: cuentas abiertas por mesa, cobro con un solo medio de pago, compras de insumos, otros gastos e informes. Es **un único archivo HTML** (`index.html`) sin librerías, fuentes ni servicios externos.

**Página publicada:** https://master-mintaka.github.io/atiks-pos/

## Qué hace

- **Servicio:** 25 puntos de venta (Mesa 1–20, Barra 1–4 y "Para llevar"). Cada punto tiene una cuenta abierta que acumula productos hasta el cobro.
- **Precios:** el precio de lista se copia a la cuenta y se puede cambiar por unidad o por línea; una cortesía es un precio de 0. Se guardan el precio de lista y el cobrado.
- **Cobro:** un solo medio de pago por cuenta: Efectivo, Nequi, Bre-B o Transferencia Bancolombia. Las cuentas canceladas o anuladas quedan registradas y no suman en los totales.
- **Gastos:** compras de insumos (qué se compró y cuánto, sin proveedor) y nómina y comisión.
- **Informes:** diario, semanal (lunes a domingo) y mensual: ventas, compras, gastos, balance de caja (ventas − compras − nómina y comisión), medios de pago, categorías y productos más vendidos. Se descargan en CSV.
- **Productos:** crear, editar precio, activar y desactivar (no se borran).
- **Respaldo:** exportar e importar JSON completo o CSV por tabla.
- **Modo claro y oscuro** con un botón arriba (por defecto oscuro).

## Dónde se guardan los datos

Esta es la parte importante:

- Al abrirla en esta página (o desde un archivo), los datos se guardan **solo en el navegador y el dispositivo donde los registras** (IndexedDB). **No se envían a ningún servidor** y **no se comparten entre dispositivos**.
- Si borras los datos del navegador, **se pierden**. Haz un respaldo JSON con frecuencia (pestaña **Respaldo**).
- Usa siempre el mismo dispositivo y el mismo navegador, y no la ventana privada.
- Dentro de Claude (como artefacto) usa la base de datos del artefacto, compartida entre dispositivos.

## Primer uso

1. Abre la página.
2. Pestaña **Respaldo** → elige `datos-base.json` (en este repositorio) → **Combinar**. Carga los 15 productos del menú con sus precios.
3. Listo: en **Mesas** toca un punto para abrir una cuenta.

## Cómo está organizado el código

Todo el código está en `index.html`, en cuatro bloques:

1. Utilidades (fechas, dinero, CSV).
2. **Capa de datos** (`Datos`): el único lugar que lee o escribe datos (`guardarVenta()`, `ventasPorFecha()`, `guardarCompra()`, etc.). Tiene dos almacenamientos intercambiables: IndexedDB y la base del artefacto de Claude.
3. Plataforma (descargas).
4. Interfaz, que solo habla con `Datos`.

Para usar otro almacenamiento (por ejemplo un servidor propio) basta con escribir otro adaptador con la misma interfaz.

## Publicar en GitHub Pages

En el repositorio: **Settings → Pages → Build and deployment → Source: Deploy from a branch → Branch: `main` / `(root)` → Save**. La página queda en `https://<usuario>.github.io/atiks-pos/`.

## Privacidad

El repositorio es público y **no contiene datos del negocio**. El `.gitignore` excluye los respaldos y los CSV de ventas, compras y gastos para que no se suban por accidente. **No subas nunca un respaldo con ventas reales.**

## Limitaciones

- Los datos no se sincronizan entre dispositivos.
- No es una PWA instalable ni garantiza funcionar sin conexión la primera vez; necesita internet para abrir la página la primera vez.
- Sin usuarios, roles, propinas, impuestos, facturación, pagos divididos ni cierre de caja.

---

<a id="english"></a>

# Atik's POS (English)

[Español](#atiks-pos)

A very simple point of sale for **Atik's Café**: open tabs per table, single-method payment, supply purchases, other expenses and reports. It is **a single HTML file** (`index.html`) with no external libraries, fonts or services.

**Live page:** https://master-mintaka.github.io/atiks-pos/

## Features

- **Service:** 25 points of sale (Table 1–20, Bar 1–4 and "Take-away"). Each point keeps one open tab that collects items until it is paid.
- **Prices:** the list price is copied to the tab and can be changed per unit or per line; a complimentary item is a price of 0. Both list and charged prices are stored.
- **Payment:** one method per tab: cash, Nequi, Bre-B or Bancolombia transfer. Cancelled or voided tabs are kept on record and excluded from totals.
- **Expenses:** supply purchases (what and how much, no supplier) plus payroll and commission.
- **Reports:** daily, weekly (Monday to Sunday) and monthly: sales, purchases, expenses, cash balance (sales − purchases − payroll and commission), payment methods, categories and best sellers. Downloadable as CSV.
- **Products:** create, edit price, activate and deactivate (never deleted).
- **Backup:** export and import a full JSON or a per-table CSV.
- **Light and dark mode** with a button in the top bar (dark by default).

## Where data is stored

This is the important part:

- When used on this page (or from a file), data is stored **only in the browser and device where you enter it** (IndexedDB). It is **never sent to a server** and **not shared between devices**.
- If you clear the browser's site data, **it is lost**. Make a JSON backup often (**Respaldo** tab).
- Always use the same device and browser, not a private window.
- Inside Claude (as an artifact) it uses the artifact's own database, which is shared across devices.

## First use

1. Open the page.
2. **Respaldo** tab → choose `datos-base.json` (in this repository) → **Combinar** (merge). It loads the 15 menu products with their prices.
3. Done: in **Mesas** tap a point to open a tab.

## Code layout

Everything lives in `index.html`, in four blocks:

1. Utilities (dates, money, CSV).
2. **Data layer** (`Datos`): the only place that reads or writes data (`guardarVenta()`, `ventasPorFecha()`, `guardarCompra()`, etc.). It has two interchangeable storages: IndexedDB and the Claude artifact database.
3. Platform (downloads).
4. UI, which only talks to `Datos`.

To use a different storage (for example your own server), write another adapter with the same interface.

## Publishing on GitHub Pages

In the repository: **Settings → Pages → Build and deployment → Source: Deploy from a branch → Branch: `main` / `(root)` → Save**. The page is served at `https://<user>.github.io/atiks-pos/`.

## Privacy

The repository is public and **contains no business data**. `.gitignore` excludes backups and the sales, purchases and expenses CSVs so they are not pushed by accident. **Never commit a backup with real sales.**

## Limitations

- Data does not sync between devices.
- It is not an installable PWA and does not guarantee offline use on first load; it needs internet to open the page the first time.
- No users, roles, tips, taxes, invoicing, split payments or cash-register closing.
