# Hashing (WIP)

Hashing is a process used to convert data of any size into a fixed-length string of characters, usually through a mathematical algorithm. Unlike encryption, which can be reversed (decrypted), hashing is a one-way function, meaning that the original data cannot be recovered from the hash.&#x20;

<figure><img src="../../../.gitbook/assets/image (2) (1) (1) (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

For example, when a file or password is hashed, any slight change in the input data will produce a completely different hash value. This makes it ideal for detecting changes in data and ensuring that files or messages haven't been altered.

***

* **Determinista**: la misma entrada siempre da el mismo resultado
* ⚡ **Rápido** de calcular
* 🧩 **Resistente a colisiones**: difícil encontrar dos entradas distintas con el mismo hash

#### 🧂 Salt

El **salt** es un valor aleatorio que se **añade a la entrada antes del hash**.\
🔐 Sirve especialmente para el almacenamiento de contraseñas, ya que evita ataques de diccionario o fuerza bruta.

💡 **Beneficio clave**: incluso si dos personas tienen la misma contraseña, sus hashes serán distintos gracias al salt único.

***

#### 🌶️ Pepper

El **pepper** funciona como el salt, pero con una diferencia clave:\
🚫 **No se almacena junto al hash** y se mantiene **secreto**.

🔒 Se añade **una capa extra de seguridad**, combinándose con la contraseña antes de aplicar el hash.

***

#### HMAC (Hash-based Message Authentication Code)

🔐 El **HMAC** combina una función hash con una **clave secreta** para garantizar:

* 🧬 **Integridad**: que los datos no fueron alterados
* 🧑‍💻 **Autenticidad**: que vienen de una fuente confiable

📌 Usos comunes:

* Firmas de API
* Verificación de mensajes entre sistemas
