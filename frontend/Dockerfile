# Image nginx:alpine choisie pour sa légèreté (~25 MB) :
# elle contient uniquement Nginx, sans OS complet ni outils inutiles.
# Pas de multi-stage nécessaire ici : le front-end est un fichier HTML statique,
# il n'y a rien à compiler ni à tester.

FROM nginx:alpine

# Supprime la config Nginx par défaut et la remplace par la nôtre
RUN rm /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Copie le fichier HTML statique
COPY index.html /usr/share/nginx/html/index.html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
