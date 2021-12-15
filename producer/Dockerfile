FROM python:2.7-onbuild
ENV PYTHONPATH /usr/src/app
WORKDIR /app
ADD producer.py /app
ADD requirements.txt /app
RUN pip install --requirement /app/requirements.txt
CMD ["python2","producer.py","-p","5672","-s","http://192.168.99.102","-m","Hello gal ya^king","-r","30"]
