<!-- ENTETE -->
[![img](https://img.shields.io/badge/Cycle%20de%20Vie-Phase%20D%C3%A9couverte-339999)](https://www.quebec.ca/gouv/politiques-orientations/vitrine-numeriqc/accompagnement-des-organismes-publics/demarche-conception-services-numeriques)
[![License](https://img.shields.io/badge/License-LiLiQ--P-blue)](LICENSE)

---

<div>
    <a target="_blank" href="https://www.quebec.ca/gouvernement/ministere/cybersecurite-numerique">
      <img src="https://github.com/CQEN-QDCE/.github/blob/main/images/mcn.png" alt="Logo du Ministère de la cybersécurité et du numérique" />
    </a>
</div>
<!-- FIN ENTETE -->

<!-- PROJECT SHIELDS -->

[![Démarche][demarche-shield]][demarche-url]

---

<!-- PROJET -->
# OpenShift Let's Encrypt Job (AWS)

Un `Job`/`cronjob` qui exécute le script Acme.sh pour générer des certificats Let's Encrypt pour l'endpoint "api" de votre cluster OpenShift, ainsi que le sous-domaine "apps" wildcard.

Ceci est seulement pour AWS (Route53) actuellement.

## Démarrage 

### Pré-requis

* [Avoir installer oc cli](https://docs.okd.io/4.10/cli_reference/openshift_cli/getting-started-cli.html)

* Avoir un cluster OpenShift v.4.10.0 ou supérieur.

* Un accès de niveau administrateur au cluster OpenShift.


### Installation

* Exécutez la commande oc login et fournissez l'URL du serveur OpenShift Container Platform (et éventuellement un jeton).


```
oc login https://Mycluster_hostName:6443
```

```
oc login --token=xxxxxxxx --server=https://Mycluster_hostName:6443

```

* Clonez ce repo 

```
git clone https://github.com/CQEN-QDCE/ocp-letsencrypt-job.git

```

* Mettez à jour le secret "cloud-dns-credentials.yaml" pour inclure votre clé secrète AWS et votre ID (un utilisateur avec des permissions Route53).

* Lancez les scripts afin d'installer un cronjob qui mettra à jour le certificat tous les 3 mois.

```
oc apply -k kustomization.yaml
```

* Construisez une image à partir du fichier Dockerfile dans le même namespace sur OpenShift.

* Mettez à jour le nom de l'image qui a été construite  "cronjob.yaml"/"job.yaml" 

* Exécutez la commande:

```
oc apply -k cronjob.yaml
```

Cela prendra quelques minutes, mais une fois la tâche réussie, vous devriez avoir de bons certs pour votre point d'accès à l'API ainsi qu'un certificat de type wildcard pour votre domaine "apps".

# Références 

https://github.com/pittar/ocp-letsencrypt-job



<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->

[demarche-url]: https://www.quebec.ca/gouv/politiques-orientations/vitrine-numeriqc/accompagnement-des-organismes-publics/demarche-conception-services-numeriques
[demarche-shield]: https://img.shields.io/badge/Lifecycle-Experimental-339999