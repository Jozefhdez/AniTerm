# 🎬 AniTerm

<p align="center">
  <img src="https://img.shields.io/badge/version-1.0.0-blue" alt="Version">
  <img src="https://img.shields.io/badge/shell-bash-green" alt="Shell">
  <img src="https://img.shields.io/badge/idioma-español-red" alt="Idioma">
  <img src="https://img.shields.io/badge/licencia-GPL--3.0-yellow" alt="Licencia">
</p>

<p align="center">
  <b>CLI para ver anime con subtítulos en español desde la terminal</b>
</p>

---

## Descripción

**AniTerm** es una herramienta de línea de comandos diseñada para la comunidad hispanohablante que permite buscar, ver y descargar anime con subtítulos en español directamente desde la terminal.

Inspirado en [ani-cli](https://github.com/pystardust/ani-cli), pero enfocado completamente en fuentes de anime en español.

## Características

- Búsqueda de anime en español
- Reproducción directa con mpv, VLC o iina
- Descarga de episodios (organizado por carpetas)
- Descarga por rangos (`-e 1-5` o `-e 4-` hasta el final)
- Velocidades de descarga rápidas (~5-8 MB/s)
- Historial de visualización
- Selección interactiva con fzf
- Sistema de fallback entre múltiples servidores
- Múltiples fuentes: MonoSchino (rápido) y AnimeFLV (alternativa)
- Modo prebuffer para reproducción sin lag
- Interfaz colorida y amigable

## 📦 Instalación

### Dependencias

**Requeridas:**
```bash
# macOS
brew install curl fzf mpv yt-dlp

# Debian/Ubuntu
sudo apt install curl fzf mpv yt-dlp

# Arch Linux
sudo pacman -S curl fzf mpv yt-dlp
```

**Opcionales (descargas más rápidas):**
```bash
# macOS
brew install aria2

# Debian/Ubuntu
sudo apt install aria2
```

### Instalar AniTerm

```bash
# Clonar el repositorio
git clone https://github.com/jozefhdez/AniTerm.git
cd AniTerm

# Dar permisos de ejecución
chmod +x aniterm

# Copiar al PATH
sudo cp aniterm /usr/local/bin/

# O para macOS con Homebrew
cp aniterm "$(brew --prefix)/bin/"
```

## 🚀 Uso

### Uso básico

```bash
# Buscar anime
aniterm naruto

# Buscar con múltiples palabras
aniterm attack on titan

# Búsqueda con guiones (recomendado)
aniterm ao-no-hako
```

### Opciones

| Opción | Descripción |
|--------|-------------|
| `-e, --episodio <n\|n-m\|n->` | Episodio específico, rango, o desde n hasta el final |
| `-d, --descargar` | Descargar episodio(s) |
| `-p, --prebuffer` | Descargar completo antes de reproducir (sin lag) |
| `-c, --continuar` | Continuar desde el historial |
| `-H, --historial` | Ver historial de visualización |
| `-D, --borrar-historial` | Eliminar historial |
| `-S, --seleccionar <n>` | Seleccionar resultado n directamente |
| `-v, --vlc` | Usar VLC como reproductor |
| `--monoschino` | Usar MonoSchino como fuente (por defecto, ~5 MB/s) |
| `--animeflv` | Usar AnimeFLV como fuente alternativa |
| `--no-detach` | Mantener reproductor en primer plano |
| `-V, --version` | Mostrar versión |
| `-h, --ayuda` | Mostrar ayuda |

### Ejemplos

```bash
# Ver episodio específico
aniterm -e 5 "ao-no-hako"

# Descargar episodio 1
aniterm -d -e 1 frieren

# Descargar episodios 1 al 5
aniterm -d -e 1-5 "demon slayer"

# Descargar desde episodio 10 hasta el final
aniterm -d -e 10- "one piece"

# Ver con prebuffer (sin interrupciones)
aniterm --prebuffer -e 1 "jujutsu kaisen"

# Usar AnimeFLV como fuente
aniterm --animeflv naruto

# Continuar el último anime
aniterm -c

# Ver historial
aniterm -H
```

### Estructura de descargas

Las descargas se organizan automáticamente:
```
~/Downloads/AniTerm/
├── Ao no Hako/
│   ├── Episodio 01.mp4
│   ├── Episodio 02.mp4
│   └── Episodio 03.mp4
├── Frieren/
│   ├── Episodio 01.mp4
│   └── Episodio 02.mp4
```

## Configuración

### Variables de entorno

```bash
# Añadir a ~/.bashrc o ~/.zshrc

# Reproductor por defecto (mpv, vlc, iina)
export ANITERM_PLAYER="mpv"

# Directorio de descargas (por defecto: ~/Downloads/AniTerm)
export ANITERM_DOWNLOAD_DIR="$HOME/Videos/Anime"

# Calidad por defecto
export ANITERM_QUALITY="1080"
```

### Archivos de datos

- **Historial:** `~/.local/share/aniterm/historial`
- **Logs:** `~/.local/share/aniterm/log`

## Fuentes de anime

| Fuente | Velocidad | Descripción |
|--------|-----------|-------------|
| MonoSchino (defecto) | ~5-8 MB/s | Servidores rápidos (mp4upload) |
| AnimeFLV | ~1-2 MB/s | Mayor catálogo, más lento |

El sistema intenta automáticamente la fuente alternativa si la principal falla.

## ⚠️ Limitaciones conocidas

- Algunos animes muy antiguos pueden tener servidores caídos
- yt-dlp no soporta todos los servidores de streaming
- El modo Syncplay requiere tener Syncplay instalado

## 📋 FAQ

**¿Cómo buscar anime con espacios?**
> Usa guiones: `aniterm ao-no-hako` o comillas: `aniterm "ao no hako"`

**¿Por qué algunos episodios no reproducen?**
> El sistema intenta múltiples servidores automáticamente. Si todos fallan, el episodio puede estar temporalmente no disponible.

**¿Cómo cambio el reproductor?**
> Usa `-v` para VLC o configura `ANITERM_PLAYER=vlc` en tu shell.

**¿Funciona en Windows?**
> Solo Linux y macOS. Para Windows usa WSL.

## Licencia

GPL-3.0 - Ver [LICENSE](LICENSE) para más detalles.