# rocket-chat-marketplace-bug-fix
 just run a mongo query and patch this shit - rocket chat marketplace upgrade update issue solve solution

Sure! Here's the **English version** of the same `README.md` so you can share it with the broader Rocket.Chat community or as an open issue/patch:

---

# 🚀 Rocket.Chat Marketplace Unlock Fix (7.x)

If you've upgraded Rocket.Chat to version `7.4.1` but the **Marketplace is still locked** or you're seeing an **incorrect version like `6.1.2`**, your database might be holding outdated info in the `rocketchat_statistics` collection.

This patch forces the correct version in the DB to match the actual deployment version, unlocking the Marketplace view.

---

## ✅ Symptoms

- 🔒 Marketplace doesn't open
- ⚠️ Message: “This workspace cannot access the marketplace because it's running an unsupported version”
- ❌ Rocket.Chat is at `7.4.1` but DB shows version `6.1.2`

---

## 🛠 Manual Fix

### 1. Access MongoDB

If you're using `docker compose`:

```bash
docker compose exec -it mongodb mongosh rocketchat
```

### 2. Update the Version

Run this MongoDB command:

```js
db.rocketchat_statistics.updateMany(
  {},
  { $set: { version: "7.4.1" } }
)
```

### 3. Restart Rocket.Chat

```bash
docker compose restart rocketchat
```

---

## 🧪 Verify

After the restart:

- Go to **Administration → Marketplace**
- You should now see the **Explore** section with apps like `WhatsApp 360Dialog`, `Rocket.Chat AI`, `ClamAV`, etc.

---

## 💡 Notes

- This fix is especially helpful after database restores or manual migrations where the `version` field wasn’t properly updated.
- Make sure your workspace is **registered and connected to Rocket.Chat Cloud** to install premium apps.

---

## ❤️ Contribute Back

Found this helpful? Open a PR, share improvements, or tell your story on the [Rocket.Chat forums](https://forums.rocket.chat).

---
Perfetto! Ecco un bel **README** markdown pronto per la community, con un tono chiaro e professionale ma diretto. Puoi incollarlo direttamente in GitHub, Gitea, o dove vuoi condividere la patch:

---

# 🚀 Rocket.Chat Marketplace Unlock Fix (7.x)

Se hai aggiornato Rocket.Chat alla versione `7.4.1` ma **il Marketplace continua a non essere accessibile** o mostra ancora una **versione errata come `6.1.2`**, è probabile che ci sia un'informazione errata nel tuo database.

Questo fix forza l'aggiornamento del campo `version` nel documento `rocketchat_statistics` per riflettere la versione reale, sbloccando così l'accesso al Marketplace.

---

## ✅ Sintomi
- 🔒 Il Marketplace non si apre
- ⚠️ Messaggio “This workspace cannot access the marketplace because it's running an unsupported version”
- ❌ Rocket.Chat in `7.4.1` ma `rocketchat_statistics.version` ancora `6.1.2`

---

## 🛠 Fix Manuale

### 1. Accedi a MongoDB
Assumendo che stai usando `docker compose`:

```bash
docker compose exec -it mongodb mongosh rocketchat
```

### 2. Aggiorna la versione
Nel prompt MongoDB esegui:

```js
db.rocketchat_statistics.updateMany(
  {},
  { $set: { version: "7.4.1" } }
)
```

### 3. Riavvia Rocket.Chat

```bash
docker compose restart rocketchat
```

---

## 🧪 Verifica

Dopo il riavvio:

- Vai su **Amministrazione → Marketplace**
- Dovresti vedere la sezione **Esplora**, con app come `WhatsApp 360Dialog`, `Rocket.Chat AI`, `ClamAV`, ecc.

---

## 💡 Note
- Questo fix è utile soprattutto in installazioni dove il campo `version` è stato mantenuto da una migrazione o restore da backup precedente.
- Assicurati che la tua istanza Rocket.Chat sia **registrata e connessa al cloud** se vuoi installare app premium.

---

## ❤️ Supporta la Community
Hai trovato utile questa guida? Apri una PR con altri fix o condividi il tuo caso sul forum ufficiale: [forums.rocket.chat](https://forums.rocket.chat)
