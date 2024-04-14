# Quadlets

## Important notes

1. I use Fedora Kinoite which has Podman pre-installed
2. These Quadlets have been tested on Fedora Kinoite 39 with Podman 4.9.4
3. Fedora uses SELinux, hence I use :Z flag for Podman's volumes. This flag will not work without SELinux

## Preparation

1. Create folders for Quadlets

```bash
mkdir -p ~/.config/containers/systemd/{chatgpt-web,stirling-pdf}
```

2. Create folders for app data

```bash
mkdir -p ~/podman/appdata/chatgpt-web/app
mkdir -p ~/podman/appdata/stirling-pdf/{tessdata,logs}
```

3. Quadlets are available in Podman 4.4+. See [release notes](https://github.com/containers/podman/releases/tag/v4.4.0). Check the version of Podman with:

```bash
podman version
```


## chatgpt-web

Build container with a Dockerfile from this Niek van der Maas' [repo](https://github.com/Niek/chatgpt-web).

```bash
cd /tmp
git clone git@github.com:Niek/chatgpt-web.git
cd chatgpt-web
podman build . -t chatgpt-web
```

## stirling-pdf

1. Download the required Tesseract files from [tessdata_fast](https://github.com/tesseract-ocr/tessdata_fast) (for fast OCR) or [tessdata](https://github.com/tesseract-ocr/tessdata) (for more accurate and slower OCR). For example,

```bash
cd ~/Downloads
wget https://github.com/tesseract-ocr/tessdata/raw/main/fin.traineddata
```

2. Place the Tesseract files into `~/podman/appdata/stirling-pdf/tessdata`.


```bash
mv ~/Downloads/fin.traineddata ~/podman/appdata/stirling-pdf/tessdata
```

## Clone repo

```bash
cd /tmp
git clone git@github.com:artur-sannikov/local-quadlets.git
mv local-quadlets/{chatgpt-web,stirling-pdf} ~/.config/containers/systemd
