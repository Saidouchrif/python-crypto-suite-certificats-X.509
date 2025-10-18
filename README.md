# 🔐 Python Crypto Suite - Certificats X.509

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://python.org)
[![Cryptography](https://img.shields.io/badge/Cryptography-Latest-green.svg)](https://cryptography.io)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## 📖 Description

Suite cryptographique complète en Python démontrant les principaux mécanismes de sécurité informatique. Ce projet implémente et illustre les concepts fondamentaux de la cryptographie moderne à travers des exemples pratiques et interactifs.

## ✨ Fonctionnalités

- 🔐 **Chiffrement Symétrique AES** - Chiffrement/déchiffrement avec Fernet
- 🔑 **Chiffrement Asymétrique RSA** - Système de clés publique/privée
- 🧾 **Certificats X.509** - Génération de certificats auto-signés
- ✍️ **Signature HMAC** - Signature et vérification d'intégrité avec HMAC-SHA256
- 📊 **Notebooks Interactifs** - Démonstrations Jupyter pour chaque composant

## 🏗️ Architecture du Projet

```
python-crypto-suite-certificats-X.509/
├── 📁 AES/                     # Chiffrement symétrique
│   ├── 📓 aes_crypto.ipynb     # Démonstration AES/Fernet
│   └── 🔑 secret.key          # Clé AES générée
├── 📁 RSA/                     # Chiffrement asymétrique
│   ├── 📓 rsa_crypto.ipynb     # Démonstration RSA
│   ├── 🔐 private_key.pem      # Clé privée RSA
│   └── 🔓 public_key.pem       # Clé publique RSA
├── 📁 Certificat X.509/        # Certificats numériques
│   ├── 📓 cert_generator.ipynb # Génération de certificats
│   ├── 📜 certificate.pem      # Certificat X.509 auto-signé
│   ├── 🔐 private_key.pem      # Clé privée du certificat
│   └── 🔓 public_key.pem       # Clé publique du certificat
├── 📁 Hmac/                    # Signature et vérification
│   ├── 📓 hmac_sign.ipynb      # Signature HMAC
│   ├── 📓 hmac_verify.ipynb    # Vérification HMAC
│   ├── 📄 message.txt          # Message à signer
│   └── ✍️ message.hmac         # Signature HMAC générée
└── 📋 README.md                # Documentation du projet
```

## 🚀 Installation

### Prérequis
- Python 3.8 ou supérieur
- pip (gestionnaire de paquets Python)
- Jupyter Notebook (optionnel, pour les démonstrations)

### Installation des dépendances

```bash
# Cloner le projet
git clone https://github.com/Saidouchrif/python-crypto-suite-certificats-X.509.git
cd python-crypto-suite-certificats-X.509

# Installer les dépendances
pip install -r requirements.txt

# Ou installer manuellement
pip install cryptography jupyter notebook
```

## 📚 Guide d'utilisation

### 1. 🔐 Chiffrement AES (Symétrique)

```python
from cryptography.fernet import Fernet

# Génération de clé
key = Fernet.generate_key()
fernet = Fernet(key)

# Chiffrement
message = b"Message secret"
encrypted = fernet.encrypt(message)

# Déchiffrement
decrypted = fernet.decrypt(encrypted)
```

**Fichiers concernés:** `AES/aes_crypto.ipynb`, `AES/secret.key`

### 2. 🔑 Chiffrement RSA (Asymétrique)

```python
from cryptography.hazmat.primitives.asymmetric import rsa, padding
from cryptography.hazmat.primitives import hashes

# Chargement des clés
with open("public_key.pem", "rb") as f:
    public_key = serialization.load_pem_public_key(f.read())

# Chiffrement avec clé publique
ciphertext = public_key.encrypt(
    message,
    padding.OAEP(
        mgf=padding.MGF1(algorithm=hashes.SHA256()),
        algorithm=hashes.SHA256(),
        label=None
    )
)
```

**Fichiers concernés:** `RSA/rsa_crypto.ipynb`, `RSA/private_key.pem`, `RSA/public_key.pem`

### 3. 🧾 Certificats X.509

```python
from cryptography import x509
from cryptography.x509.oid import NameOID
import datetime

# Création d'un certificat auto-signé
subject = issuer = x509.Name([
    x509.NameAttribute(NameOID.COUNTRY_NAME, u"MA"),
    x509.NameAttribute(NameOID.ORGANIZATION_NAME, u"Mundipolis"),
    x509.NameAttribute(NameOID.COMMON_NAME, u"mundipolis.ma"),
])

certificate = x509.CertificateBuilder().subject_name(
    subject
).issuer_name(
    issuer
).public_key(
    public_key
).serial_number(
    x509.random_serial_number()
).not_valid_before(
    datetime.datetime.now(datetime.UTC)
).not_valid_after(
    datetime.datetime.now(datetime.UTC) + datetime.timedelta(days=365)
).sign(private_key, hashes.SHA256())
```

**Fichiers concernés:** `Certificat X.509/cert_generator.ipynb`, `Certificat X.509/certificate.pem`

### 4. ✍️ Signature HMAC

```python
import hmac
import hashlib
import base64

# Signature
secret_key = b'secret_key_123'
hmac_digest = hmac.new(secret_key, message, hashlib.sha256).digest()
signature = base64.b64encode(hmac_digest)

# Vérification
computed_hmac = hmac.new(secret_key, message, hashlib.sha256).digest()
is_valid = hmac.compare_digest(computed_hmac, base64.b64decode(signature))
```

**Fichiers concernés:** `Hmac/hmac_sign.ipynb`, `Hmac/hmac_verify.ipynb`

## 🔧 Schémas de Données

### Schéma Global du Projet

```json
{
  "project": {
    "name": "python-crypto-suite-certificats-X.509",
    "version": "1.0.0",
    "type": "cryptographic-suite",
    "components": [
      {
        "name": "AES",
        "type": "symmetric-encryption",
        "algorithm": "AES-256 (Fernet)",
        "files": ["aes_crypto.ipynb", "secret.key"]
      },
      {
        "name": "RSA",
        "type": "asymmetric-encryption",
        "algorithm": "RSA-2048",
        "files": ["rsa_crypto.ipynb", "private_key.pem", "public_key.pem"]
      },
      {
        "name": "X509",
        "type": "digital-certificates",
        "standard": "X.509v3",
        "files": ["cert_generator.ipynb", "certificate.pem", "private_key.pem", "public_key.pem"]
      },
      {
        "name": "HMAC",
        "type": "message-authentication",
        "algorithm": "HMAC-SHA256",
        "files": ["hmac_sign.ipynb", "hmac_verify.ipynb", "message.txt", "message.hmac"]
      }
    ],
    "dependencies": {
      "cryptography": ">=41.0.0",
      "jupyter": ">=1.0.0"
    }
  }
}
```

### Schémas par Composant

#### 🔐 AES Component Schema
```json
{
  "aes_component": {
    "type": "symmetric_encryption",
    "algorithm": "AES-256",
    "implementation": "Fernet (cryptography library)",
    "key_format": "base64-encoded 32-byte key",
    "files": {
      "aes_crypto.ipynb": {
        "type": "jupyter_notebook",
        "purpose": "demonstration and implementation",
        "functions": ["key_generation", "encryption", "decryption"]
      },
      "secret.key": {
        "type": "binary_key_file",
        "format": "base64",
        "size": "44 bytes",
        "encoding": "UTF-8"
      }
    },
    "operations": {
      "encrypt": {
        "input": "bytes",
        "output": "base64_encoded_bytes",
        "method": "fernet.encrypt()"
      },
      "decrypt": {
        "input": "base64_encoded_bytes",
        "output": "bytes",
        "method": "fernet.decrypt()"
      }
    }
  }
}
```

#### 🔑 RSA Component Schema
```json
{
  "rsa_component": {
    "type": "asymmetric_encryption",
    "algorithm": "RSA",
    "key_size": 2048,
    "padding": "OAEP with SHA-256",
    "files": {
      "rsa_crypto.ipynb": {
        "type": "jupyter_notebook",
        "purpose": "RSA encryption/decryption demonstration",
        "operations": ["key_loading", "encryption", "decryption"]
      },
      "private_key.pem": {
        "type": "pem_private_key",
        "format": "PKCS#1 PEM",
        "encryption": "none",
        "size": "2048 bits"
      },
      "public_key.pem": {
        "type": "pem_public_key",
        "format": "SubjectPublicKeyInfo PEM",
        "size": "2048 bits"
      }
    },
    "security": {
      "padding_scheme": "OAEP",
      "mgf": "MGF1",
      "hash_algorithm": "SHA-256",
      "max_message_size": "190 bytes (for 2048-bit key)"
    }
  }
}
```

#### 🧾 X.509 Certificate Schema
```json
{
  "x509_component": {
    "type": "digital_certificate",
    "standard": "X.509v3",
    "signature_algorithm": "SHA-256 with RSA",
    "files": {
      "cert_generator.ipynb": {
        "type": "jupyter_notebook",
        "purpose": "certificate generation and key pair creation",
        "outputs": ["private_key.pem", "public_key.pem", "certificate.pem"]
      },
      "certificate.pem": {
        "type": "x509_certificate",
        "format": "PEM",
        "version": "v3",
        "validity_period": "365 days",
        "subject": {
          "country": "MA",
          "state": "CASABLANCA",
          "locality": "Casablanca",
          "organization": "Mundipolis",
          "common_name": "mundipolis.ma"
        },
        "extensions": {
          "subject_alternative_name": "mundipolis.ma"
        }
      }
    },
    "certificate_fields": {
      "serial_number": "random_generated",
      "issuer": "self_signed",
      "not_before": "current_utc_time",
      "not_after": "current_utc_time + 365_days",
      "public_key_algorithm": "RSA",
      "signature_algorithm": "SHA256withRSA"
    }
  }
}
```

#### ✍️ HMAC Component Schema
```json
{
  "hmac_component": {
    "type": "message_authentication_code",
    "algorithm": "HMAC-SHA256",
    "purpose": "message_integrity_and_authenticity",
    "files": {
      "hmac_sign.ipynb": {
        "type": "jupyter_notebook",
        "purpose": "message signing with HMAC",
        "input": "message.txt",
        "output": "message.hmac"
      },
      "hmac_verify.ipynb": {
        "type": "jupyter_notebook",
        "purpose": "signature verification",
        "inputs": ["message.txt", "message.hmac"],
        "output": "verification_result"
      },
      "message.txt": {
        "type": "plain_text",
        "content": "sample message to be signed",
        "encoding": "UTF-8"
      },
      "message.hmac": {
        "type": "hmac_signature",
        "format": "base64_encoded",
        "algorithm": "HMAC-SHA256",
        "key": "secret_key_123"
      }
    },
    "process": {
      "signing": {
        "steps": [
          "load_message_from_file",
          "apply_hmac_with_secret_key",
          "encode_result_in_base64",
          "save_signature_to_file"
        ]
      },
      "verification": {
        "steps": [
          "load_message_and_signature",
          "compute_hmac_of_message",
          "compare_with_stored_signature",
          "return_verification_result"
        ]
      }
    }
  }
}
```

## 🛡️ Sécurité et Bonnes Pratiques

### Recommandations de Sécurité

- **🔐 Gestion des Clés**: Ne jamais stocker les clés privées en plain text en production
- **🔄 Rotation des Clés**: Implémenter une rotation régulière des clés cryptographiques
- **🛡️ Validation**: Toujours valider les certificats et signatures avant utilisation
- **📝 Audit**: Maintenir des logs d'audit pour toutes les opérations cryptographiques

### Limitations du Projet

- **🎓 Éducatif**: Ce projet est à des fins éducatives et de démonstration
- **🔒 Production**: Ne pas utiliser tel quel en environnement de production
- **🔑 Clés**: Les clés générées sont stockées sans protection supplémentaire

## 📋 Dépendances

```txt
cryptography>=41.0.0
jupyter>=1.0.0
notebook>=6.0.0
```

## 🤝 Contribution

1. Fork le projet
2. Créer une branche feature (`git checkout -b feature/nouvelle-fonctionnalite`)
3. Commit les changements (`git commit -am 'Ajout nouvelle fonctionnalité'`)
4. Push vers la branche (`git push origin feature/nouvelle-fonctionnalite`)
5. Créer une Pull Request

## 📄 Licence

Ce projet est sous licence MIT. Voir le fichier `LICENSE` pour plus de détails.

## 👥 Auteurs

- **Équipe Crypto Suite** - *Développement initial*

## 🙏 Remerciements

- Bibliothèque [Cryptography](https://cryptography.io/) pour les implémentations cryptographiques
- Communauté Python pour les outils et ressources
- Standards X.509 et RFC pour les spécifications cryptographiques

---

**⚠️ Avertissement**: Ce projet est destiné à l'apprentissage et à la démonstration. Pour un usage en production, consultez un expert en sécurité et suivez les meilleures pratiques de l'industrie.
