FROM python:3.9

# Install Poetry
RUN curl -sSL https://install.python-poetry.org | python3 -

# Set Poetry environment variables
ENV POETRY_HOME=/opt/poetry
ENV POETRY_VIRTUALENVS_IN_PROJECT=true
ENV PATH="$POETRY_HOME/bin:$PATH"

WORKDIR /app

# Copy only the dependency files to cache dependencies
COPY pyproject.toml poetry.lock ./

# Install dependencies
RUN poetry install --no-root --no-dev

# Copy the rest of the application
COPY . .

# Run the application
CMD ["poetry", "run", "uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]

EXPOSE 8000
