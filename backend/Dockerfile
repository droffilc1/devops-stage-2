FROM python:3.9

# Install Poetry
RUN curl -sSL https://install.python-poetry.org | python3 -

# Set Poetry environment variables
ENV POETRY_HOME=/root/.local
ENV PATH="$POETRY_HOME/bin:$PATH"

# Verify Poetry installation and PATH
RUN echo $(PATH)
RUN poetry --version

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
