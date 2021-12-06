FROM ubuntu:20.04

RUN apt-get update  && apt-get install -y \
			build-essential \
			python-dev \
			python3-pip 

COPY requirements.txt /usr/src/app/
RUN pip install --no-cache-dir -r /usr/src/app/requirements.txt
COPY app.py /usr/src/app/
EXPOSE 5000
CMD ["python3", "/usr/src/app/app.py"]
