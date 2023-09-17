FROM python:3.10-bullseye
RUN apt-get update
RUN apt-get install -y linux-headers-generic
RUN apt-get update && apt-get install bash gcc musl-dev -y libjpeg-dev -y zlib1g-dev libmariadb-dev -y libffi-dev -y python3-dev
RUN apt-get install -y wkhtmltopdf

COPY requirements.txt /requirements.txt
RUN pip install --upgrade pip
RUN pip install -r requirements.txt
RUN rm /usr/bin/mysql*
COPY uwsgi.ini /uwsgi.ini
RUN pip freeze > newreqs.txt

ENV XDG_RUNTIME_DIR=/run/user/"${UID}"

EXPOSE 8000
# start server
CMD python manage.py runserver
#CMD ["uwsgi", "--ini", "/uwsgi.ini"]
