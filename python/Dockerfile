FROM python:3.12-slim AS dev
WORKDIR /app
COPY requirements.txt ./
RUN pip install --prefix=/install -r requirements.txt

FROM python:3.12-slim AS prod
WORKDIR /app
COPY --from=dev /install /usr/local
COPY ./app ./
EXPOSE 8000
CMD ["uvicorn", "main:app","--host","0.0.0.0","--port","8000"]