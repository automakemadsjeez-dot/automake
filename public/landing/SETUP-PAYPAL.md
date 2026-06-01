# Configurar PayPal Subscriptions en Automake

## 1. Cuenta PayPal Business
- https://www.paypal.com/bizsignup
- Verificá email + cuenta bancaria.

## 2. Generar Client ID
- Developer Dashboard: https://developer.paypal.com/dashboard/applications/live
- "Apps & Credentials" → "Create App" → tipo **Merchant**
- Copiá el **Client ID** de Live (no Sandbox).
- En `public/landing/index.html` reemplazá:
  ```
  https://www.paypal.com/sdk/js?client-id=sb&...
  ```
  por tu Client ID:
  ```
  https://www.paypal.com/sdk/js?client-id=AaBbCcDd...&currency=USD&intent=subscription&vault=true
  ```

## 3. Crear Subscription Plans
PayPal exige primero un **Product**, después **Plans** colgando del Product.

Dashboard → **Pay with PayPal** → **Subscriptions** → **Plans** → **+ Create plan**

Creá 6 planes (3 tiers × mensual/anual):

| Plan key | Nombre | Precio USD | Ciclo |
|---|---|---|---|
| starter / monthly | Automake Starter mensual | 29.00 | Monthly |
| starter / yearly  | Automake Starter anual   | 276.00 (23×12) | Yearly |
| pro / monthly     | Automake Pro mensual     | 79.00 | Monthly |
| pro / yearly      | Automake Pro anual       | 756.00 (63×12) | Yearly |
| scale / monthly   | Automake Scale mensual   | 199.00 | Monthly |
| scale / yearly    | Automake Scale anual     | 1908.00 (159×12) | Yearly |

Copiá cada **Plan ID** (`P-XXXXXXXXXXXXXX`).

## 4. Pegar los Plan IDs en el código
En `public/landing/index.html`, buscá `window.AUTOMAKE_PAYPAL_PLANS` y reemplazá:

```js
window.AUTOMAKE_PAYPAL_PLANS = {
  starter: { monthly: 'P-XXX', yearly: 'P-YYY' },
  pro:     { monthly: 'P-XXX', yearly: 'P-YYY' },
  scale:   { monthly: 'P-XXX', yearly: 'P-YYY' }
};
```

## 5. Webhook (recomendado, para activar/desactivar cuentas)
En Developer Dashboard → tu App → **Webhooks** → **Add Webhook**:
- URL: `https://automake-production.up.railway.app/webhooks/paypal`
- Eventos suscribirse a:
  - `BILLING.SUBSCRIPTION.ACTIVATED`
  - `BILLING.SUBSCRIPTION.CANCELLED`
  - `BILLING.SUBSCRIPTION.SUSPENDED`
  - `PAYMENT.SALE.COMPLETED`

⚠️ Falta implementar el endpoint en Rails. Cuando lo hagamos, agregaremos un controller `PaypalWebhooksController` que reciba estos eventos y marque `account.paypal_subscription_status`.

## 6. Branding del dashboard Chatwoot
Para que el dashboard también se vea Automake (no Chatwoot azul):
1. Loguéate como SuperAdmin en `/super_admin`
2. Andá a **Account Settings** → **Branding**
3. Cambiá el color primario a `#6366F1` (iris) o `#A855F7` (amethyst)
4. Subí logo si querés (los `/brand-assets/*.svg` ya están servidos)

## 7. SMTP — verificar dominio en Resend
Para que los emails de Automake salgan desde un dominio tuyo (no `onboarding@resend.dev` sandbox):
1. https://resend.com/domains → Add Domain
2. Configurá los 3 records DNS (SPF, DKIM, MX) que te muestre
3. Esperá verificación (~5 min)
4. Cambiá la env `MAILER_SENDER_EMAIL` en Railway a `Automake <no-reply@tudominio.com>`
