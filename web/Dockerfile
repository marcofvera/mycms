FROM python:2.7
ENV PYTHONUNBUFFERED 1
COPY requirements.txt .
RUN pip install -r requirements.txt
RUN mkdir /code
WORKDIR /code
CMD ["python", "manage.py", "runserver", "0.0.0.0:80"]
