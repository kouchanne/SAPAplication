FROM python:3.6

ENV LANG C.UTF-8
ENV TZ Asia/Tokyo

COPY ./python /var/www

WORKDIR /var/www/
RUN pip install --upgrade pip

RUN pip install -r requirements.txt

CMD ["uwsgi","--ini","/var/www/uwsgi.ini"]