FROM python:3.10-slim

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

WORKDIR /code

RUN apt-get update \
    && apt-get install -y --no-install-recommends gcc libpq-dev curl build-essential \
    && rm -rf /var/lib/apt/lists/*

RUN curl -sSL https://install.python-poetry.org | python3 - && \
    ln -s /root/.local/bin/poetry /usr/local/bin/poetry

COPY pyproject.toml poetry.lock /code/

RUN poetry config virtualenvs.create false && poetry install --no-root --only main

COPY . /code/

CMD ["poetry", "run", "python", "manage.py", "runserver", "0.0.0.0:8000"]