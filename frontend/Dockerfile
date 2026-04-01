# On utilise nginx:1.25-alpine comme image de base.
# Alpine = image minimaliste (~5 MB), ce qui est largement suffisant pour servir
# des fichiers statiques. Pas besoin de Node.js dans cette image.

FROM nginx:1.25-alpine

# Copie de la page HTML dans le répertoire servi par Nginx par défaut
COPY index.html /usr/share/nginx/html/index.html

# Remplacement de la configuration Nginx par défaut par notre configuration
# personnalisée (avec le proxy_pass vers le back-end)
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
