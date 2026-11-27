# SSS2026
> [!NOTE]
> Questa è una repo GitHub dedicata al corso "Strumenti di Sviluppo Software - CICD"

## Esercitazione 1 - Git
- clonare questo repository in una cartella locale del proprio pc con `git clone <url_repo>`
- provare una serie di comandi per fare pratica con Git, tra cui:
  - `commit`
  - `push` e `pull`
  - `branch`
  - `merge`
- risolvere un conflitto sul branch `main` 
  - si può modificare la stessa riga dello stesso file da due branch diversi, poi fare il merge

## Esercitazione 2 - Docker
- creare dei file `.html` (contenuto a piacere) situati nella cartella `2-esercitazioneDocker`
- creare un `Dockerfile` a partire dall'immagine di `nginx:alpine`, che deve copiare e servire i file html creati al punto precedente
- fare la build dell'immagine associata al `Dockerfile` 
  ```shell
  docker build -t <nome_immagine> ./2-esercitazioneDocker/
  ```
- avviare il container
  ```shell
  docker run -d -p 8080:80 --name <nome_container> <nome_immagine>
  ```
- aprire sul browser http://localhost:8080
- provare i comandi principali della Docker CLI
- rendere dinamici i file `.html` (aggiungere del codice `JavaScript`)
  - (esempio: creare un form di login)

## Esercitazione 3 - WebApi
- clonare e avviare (seguendo le istruzioni del file `README.md`) la repo GitHub [SomeBankingApp](https://github.com/mmenapace/SomeBankingApp)
- avviare una rete docker
  ```shell
  docker network <nome_rete>
  ```
- creare un `Dockerfile` per il frontend
- creare un `Dockerfile` per il backend
- buildare manualmente le immagini dei due container
  - frontend: 
    ```shell
    docker build -t <nome_immagine_frontend> ./3-esercitazioneWebApi/frontend/
    ```
  - backend:
    ```shell
    docker build -t <nome_immagine_backend> ./3-esercitazioneWebApi/backend/
    ``` 
- avviare i rispettivi container 
  - frontend:
    ```shell
    docker run -d --name <nome_container_frontend> --network <nome_rete> -p 80:80 <nome_immagine_frontend>
    ```
  - backend:
    ```shell
    docker run -d --name <nome_container_backend> --network <nome_rete> -p 80:80 <nome_immagine_backend>
    ```
- visitare 
	1. il sito http://localhost per vedere il frontend dell'app
	2. il sito http://localhost:8000/docs per vedere il backend dell'app

## Esercitazione 4 - Docker Compose
- modificare i `Dockerfile` di frontend e backend dell'esercitazione precedente 
  - devono clonare la repo GitHub [SomeBankingApp](https://github.com/mmenapace/SomeBankingApp) nella fase di build
- buildare le immagini di frontend e backend
  ```shell
  docker build -t banking-frontend ./4-esercitazioneDockerCompose/frontend/
  docker build -t banking-backend ./4-esercitazioneDockerCompose/backend/
  ```
- creare un terzo `Dockerfile` per il reverse-proxy
- configurare il reverse-proxy tramite un file `nginx.conf`
- buildare l'immagine di reverse-proxy
  ```shell
  docker build -t banking-reverse-proxy ./4-esercitazioneDockerCompose/reverse-proxy/
  ```
- creare il `docker-compose.yaml` che gestisce tutti i servizi dell'applicazione (frontend, backend, reverse-proxy)
- eseguire `docker compose up` per avviare simultaneamente tutti e tre i container

> [!IMPORTANT]
> in questo caso sono stati già indicati i nomi delle immagini da utilizzare nella fase di build perché vengono anche riutilizzati nel file `docker-compose.yaml`. Quindi, non possono essere cambiati, ma devono essere utilizzati li stessi

## Esercitazione 5 - Jenkins
- installare Jenkins tramite docker seguendo la [guida](https://www.jenkins.io/doc/book/installing/docker/)
- visitare http://localhost:8080 
- inizializzare la nuova istanza locale, creando un account admin e scegliendo l'installazione di plugin aggiuntivi suggeriti
- creare un file `5-esercitazioneJenkins/jenkins/Jenkinsfile` in cui viene fatta la build dei container di frontend e backend (dell'esercitazione scorsa)
- creare una nuova pipeline `build-frontend-backend` in cui inserire i seguenti campi:
  - Definition: Pipeline script from SCM
  - SCM: Git
  - Repository URL: url di questa repo 
  - Credentials: none
  - Branch Specifier: `*/main` 
  - Script Path: `5-esercitazioneJenkins/jenkins/Jenkinsfile`
- controllare in `Stage view` e `Console Output` che sia andato tutto bene


