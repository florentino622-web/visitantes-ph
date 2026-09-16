# Visitantes — App de Inquilinos

App para que cada inquilino registre a sus visitantes (nombre, cédula, fechas de estadía,
descripción) y genere un código QR para enviarle. El visitante muestra ese QR en portería
y el portero lo escanea con su propia app para verificar el acceso al instante.

Esta app usa el **mismo proyecto de Firebase** que la app de portería — no hay que crear
nada nuevo, solo publicarla.

---

## Requisito previo

Debes haber hecho ya el **Paso 2** y **Paso 3** del README de la app de portería
(`porteria-app-cloud`): base de datos creada, reglas publicadas, y el proveedor
**"Anónimo"** activado en Authentication (además de correo/contraseña).

Si no activaste "Anónimo" todavía:
1. Firebase console → Authentication → Sign-in method.
2. Busca **"Anonymous"** → Activar → Guardar.

Sin este paso, la app de inquilinos no va a poder guardar nada (dará error de permisos).

## Publicar en GitHub Pages

Igual que con la app de portería, pero en un **repositorio aparte** (por ejemplo `visitantes-ph`),
para que cada una tenga su propio link:

1. Crea un nuevo repositorio en GitHub, público, por ejemplo `visitantes-ph`.
2. Sube **todos los archivos de esta carpeta** con "Add file → Upload files".
3. Settings → Pages → Branch: main / (root) → Save.
4. Espera 1-2 minutos. Tu link va a quedar como:

   ```
   https://tu-usuario.github.io/visitantes-ph/
   ```

5. Comparte ese link con todos los inquilinos (por el grupo de WhatsApp del edificio, cartelera, etc.)
   para que lo guarden en su celular (Chrome → menú ⋮ → "Instalar aplicación").

## Cómo la usan los inquilinos

1. Abren el link (o la app instalada).
2. La primera vez, les pide su **número de apartamento** (solo para etiquetar sus visitantes,
   no es una contraseña).
3. Llenan: nombre del visitante, cédula, fecha de inicio y fin de la estadía, y una descripción
   opcional.
4. Tocan **"Generar código QR"**.
5. Les aparece el QR en pantalla, con botones para **Descargar** la imagen o **Compartir**
   directo (por WhatsApp, etc.) — ya con un mensaje armado para el visitante.
6. El visitante muestra ese QR (o la cédula) en portería al llegar.

## Ya el portero ve todo automático

En cuanto un inquilino genera un QR, ese visitante **ya aparece en la app de portería**
(pestaña Registro) sin que el portero tenga que hacer nada — la sincronización es en tiempo real.

## Seguridad — qué SÍ y qué NO puede hacer un inquilino

Por diseño (ver las reglas de Firestore del README de portería):

- ✅ Puede crear un visitante nuevo.
- ✅ Puede volver a registrar (actualizar) un visitante que ya había creado antes.
- ❌ NO puede ver la lista de otros inquilinos ni de otros apartamentos.
- ❌ NO puede ver ni descargar fotos de nadie.
- ❌ NO puede editar ni borrar registros de tipo "inquilino".
- ❌ NO puede editar el registro de un visitante creado por otro apartamento.

El campo "apartamento" que escribe el inquilino **no está verificado** — es solo una etiqueta
de buena fe para identificar quién trajo al visitante, no un inicio de sesión real. Si en el
futuro quieres verificación real por apartamento (que cada quien solo pueda registrar a nombre
de su propio apto con una cuenta), es posible, pero requiere crear una cuenta por apartamento
en Firebase Authentication — dile a Claude si quieres avanzar a esa versión.
