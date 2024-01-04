FROM alpine:3.11 as builder

WORKDIR /app

ENV VIRTUAL_ENV=/opt/venv

RUN apk update && \
    apk add python2 python2-dev py2-pip && \
    pip install virtualenv && \
    virtualenv $VIRTUAL_ENV

ENV PATH="/opt/venv/bin:$PATH"


COPY ./flask-app/requirements.txt ./flask-app/app.py ./

RUN pip install -r requirements.txt 



FROM alpine:3.11 

WORKDIR /app

RUN apk update && \
    apk add python2

COPY --from=builder /opt/venv /opt/venv
COPY --from=builder /app .

ENV PATH="/opt/venv/bin:$PATH"

EXPOSE 5000

ENTRYPOINT ["python", "./app.py"]