# Iris: cómo publicarla en tu propia web

Iris tiene dos partes:

- `public/index.html`: la página que ven tus usuarios.
- `api/ask.js`: una función de servidor que envía la pregunta a Claude con tu clave. La clave nunca llega al navegador.

## 1. Consigue tu clave de API

1. Entra en https://console.anthropic.com y crea una cuenta.
2. En **Billing**, añade saldo (cada pregunta cuesta unos céntimos).
3. En **Limits**, pon un límite de gasto mensual para no llevarte sorpresas.
4. En **API Keys**, crea una clave y cópiala. Empieza por `sk-ant-`. No la compartas con nadie.

## 2. Publica en Vercel (gratis)

1. Crea una cuenta en https://vercel.com.
2. La forma más fácil: sube esta carpeta a un repositorio de GitHub y en Vercel pulsa **Add New → Project** e impórtalo.
   (Alternativa sin GitHub: instala Vercel CLI y ejecuta `npx vercel` dentro de la carpeta.)
3. En **Framework Preset** deja **Other**. No hace falta tocar nada más.
4. Antes de publicar, en **Environment Variables** añade:
   - `ANTHROPIC_API_KEY` = tu clave `sk-ant-...`
5. Pulsa **Deploy**. Vercel te dará un enlace tipo `iris-tunombre.vercel.app` que puede abrir cualquiera.

## Ajustes opcionales (también como Environment Variables)

| Variable | Para qué sirve | Por defecto |
|---|---|---|
| `IRIS_MODEL` | Modelo de Claude. `claude-haiku-5-5` es más barato; `claude-sonnet-5-5` cita mejor. | `claude-sonnet-5-5` |
| `IRIS_LIMIT_PER_HOUR` | Preguntas máximas por persona (IP) y hora. | `20` |

Si cambias una variable, vuelve a desplegar desde **Deployments → Redeploy**.

## Cosas a tener en cuenta

- Los versículos los escribe la IA. Son muy precisos en pasajes conocidos, pero cada tarjeta tiene el enlace "Leer el contexto (NVI)" para comprobarlos.
- Si quieres citar la NVI en una web pública, Biblica permite citar hasta 500 versículos sin pedir permiso, siempre que se indique la fuente (la página ya muestra "NVI" en cada cita).
- El historial de cada persona se guarda solo en su propio navegador.
- Para cambiar textos, colores o los temas sugeridos, edita `public/index.html`. Para cambiar cómo responde Iris, edita el texto `SYSTEM` en `api/ask.js`.
