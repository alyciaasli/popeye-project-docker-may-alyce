FROM python
WORKDIR /app
COPY requirements.txt /app/
RUN apt-get update && apt-get install -y python3-pip
RUN pip3 install -r requirements.txt
COPY . /app/
EXPOSE 80
CMD ["flask", "run", "--host=0.0.0.0", "--port=80"]
