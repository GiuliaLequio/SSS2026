FROM python

RUN apt-get update && apt-get install -y git
RUN git clone https://github.com/mmenapace/SomeBankingApp.git /app

WORKDIR /app/backend
# bisogna aggiungere l'installazione manuale di fastapi perchè non è presente nel requirements.txt nella repo originale
RUN pip install -r requirements.txt && pip install fastapi

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
