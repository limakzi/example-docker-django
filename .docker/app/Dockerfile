FROM python:3.12-slim-bookworm AS builder

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

EXPOSE 8000
WORKDIR /app 

RUN apt -y update && \
    apt -y install build-essential libpq-dev

COPY requirements.txt /app
RUN pip3 install -r requirements.txt --root-user-action=ignore --no-cache-dir
ENTRYPOINT ["python3"] 

FROM builder AS development
CMD ["manage.py", "runserver", "0.0.0.0:8000"]

FROM builder AS production
CMD ["gunicorn", "--bind", ":8000", "--workers", "3", "site.wsgi:application"]
