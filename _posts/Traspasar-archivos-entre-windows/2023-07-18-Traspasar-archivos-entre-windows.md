---
title: Traspasar archivos entre Windows y Linux 🔒
published: true
---

Traspasar archivos entre PCs Windows y Linux es sumamente fácil, ya que lo único que tenemos que hacer es con el Windows subir un archivo a una web temporal y con el otro descargar el archivo. Dicho esto podemos empezar con la guía de traspaso de archivos entre Windows y Linux:
# Requerimientos

Los requerimientos necesarios para poder realizar este procedimiento son:

- Instalar wget
- Windows 10/11
- Tener linux actualizado
- Tener python3 instalado

Para instalar wget lo primero que tienes que hacer es entrar en un cmd desde el PC Windows, después, tendrás que escribir lo siguiente:
```powershell

pip3 install wget

```

Y con esto ya estarías listo para poder empezar la guía.

# GUIA

Para empezar debemos posicionarnos en la ruta en la que esté el archivo que queramos traspasar desde el PC Windows, y lo que vamos a hacer es subir el archivo a una web temporal que nosotros mismos crearemos, esto se haría de la siguiente manera:

```powershell

python3 -m http.server 8080

```

También tendrás que saber cuál es la ip privada del PC Windows. Para ello, tendrás que abrir el cmd y escribir “ipconfig” y buscar el tipo de conector wifi que tengas actualmente en uso, el mío por ejemplo sería el siguiente:

<figure>
<img src="/assets/img/ipconfig.png" alt="image">
</figure>

De esa imagen, mi ip privada sería la' 192.168.0.26’ ya que es el de la ‘Dirección IPv4’.

Después de realizar esta acción en el PC Windows, lo que debemos hacer desde el PC Linux es recoger el archivo, posicionarte en la ruta que quieras que se guarde tu archivo. Después de esto, deberás escribir el siguiente comando:

```powershell
python3 -m wget http://(ip privada del PC Windows):8080/(nombre del archivo que quieras descargar)

```

# Posibles Errores

- No haberte posicionado en la ruta del archivo antes de crear la web temporal
- No escribir bien el nombre del archivo que quieres descargas, esto sucedería en el momento de recoger el archivo de la web temporal
- No haber instalado los requerimientos

# Fin

Espero que esta guía para traspasar archivos entre Windows y Linux te haya servido, si no es así o te ha surgido algún tipo de problema no dudes en contactar conmigo kuentavj@gmail.com
