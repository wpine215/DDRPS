FROM python:3.8.0-buster

WORKDIR /app/backend/

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Install python dependencies
COPY requirements.txt /app/backend
RUN pip3 install --upgrade pip
RUN pip3 install -r requirements.txt

# Copy remaining files over
COPY . /app/backend

EXPOSE 8000
CMD ["python3", "manage.py", "runserver", "0.0.0.0:8000"]