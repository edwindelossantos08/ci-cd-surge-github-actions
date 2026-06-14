# Despliegue continuo con GitHub Actions + Surge.sh

Página web estática desplegada automáticamente a [Surge.sh](https://surge.sh) mediante un workflow de **GitHub Actions** cada vez que se hace push a la rama `main`.

## Stack

- HTML5 / CSS3
- Git + GitHub
- GitHub Actions (CI/CD)
- Surge.sh (hosting estático)

## Estructura del proyecto

```
.
├── .github/
│   └── workflows/
│       └── main.yaml      # Pipeline de despliegue automático
├── .surgeignore           # Archivos ignorados al publicar en Surge
├── index.html             # Página principal
└── README.md
```

## Configuración de secrets en GitHub

En el repositorio: **Settings → Secrets and variables → Actions → New repository secret**

| Secret         | Valor                                                |
| -------------- | ---------------------------------------------------- |
| `SURGE_LOGIN`  | Tu correo registrado en Surge                        |
| `SURGE_TOKEN`  | Token obtenido con `surge token`                     |
| `SURGE_DOMAIN` | Dominio destino, por ejemplo `mi-proyecto.surge.sh`  |

## Cómo obtener el token de Surge

```bash
npm install -g surge
surge login
surge token
```

## Flujo CI/CD

1. Haces `git push` a la rama `main`
2. GitHub Actions ejecuta el workflow `main.yaml`
3. El runner instala Surge e invoca `surge ./ <dominio> --token <token>`
4. La página queda publicada en `https://<dominio>.surge.sh`

---

Autor: **Bryan Peguero Camilo**
