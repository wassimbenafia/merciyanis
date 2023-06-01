FROM python:3.7-alpine

WORKDIR /usr/src/app

RUN pip install requests==2.19.1
RUN pip install apscheduler==3.5.3
RUN pip install geopy==1.18.1

CMD ["python", "boot.py"]
