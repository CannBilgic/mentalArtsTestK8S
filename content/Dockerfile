FROM python:3.10-alpine

WORKDIR /app

COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt

COPY api/ api/

EXPOSE 8000

CMD ["python", "api/app.py"]