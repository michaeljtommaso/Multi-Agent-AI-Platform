FROM python:3.12-slim
WORKDIR /srv
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
# playwright_browse needs a browser plus the system libraries it links against.
# Playwright's own installer needs libatomic1 before it can run at all.
# --only-shell installs just the headless build, which is all the tool launches.
RUN apt-get update && apt-get install -y --no-install-recommends libatomic1 \
    && playwright install --with-deps --only-shell chromium \
    && rm -rf /var/lib/apt/lists/*
COPY . .
EXPOSE 8000
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]
