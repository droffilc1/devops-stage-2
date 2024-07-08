FROM python:3.9

# Install Poetry
RUN curl -sSL https://install.python-poetry.org | python3 -

# Set Poetry environment variables
ENV POETRY_HOME=/opt/poetry
ENV POETRY_VIRTUALENVS_IN_PROJECT=true
ENV PATH="$POETRY_HOME/bin:$PATH"

# Verify Poetry installation and PATH
RUN echo $(PATH)
RUN poetry --version

WORKDIR /app

# Copy only the dependency files to cache dependencies
COPY pyproject.toml poetry.lock ./

# Install dependencies
RUN poetry install

# Set up the database with the necessary tables
RUN poetry run bash ./prestart.sh

# Copy the rest of the application
COPY . .

# Run the application
CMD ["poetry", "run", "uvicorn", "app.main:app", "--reload"]

EXPOSE 8000
