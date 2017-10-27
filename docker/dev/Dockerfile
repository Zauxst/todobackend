FROM zauxst/todobackend-base:latest
LABEL maintainer="zauxst@gmail.com" \ 
    com.example.label.name="Zauxst" \
    version="0.1"

# Install dev/build dependenies
RUN apt-get update && \
    apt-get install -qy python-dev

# Actovate virtual environment and install wheel support
RUN . /appenv/bin/activate && \
    pip install wheel --upgrade

# PIP environment variables (NOTE: must be set after installing wheel)
ENV WHEELHOUSE=/wheelhouse PIP_WHEEL_DIR/wheelhouse PIP_FIND_LINKS=/wheelhouse XDG_CACHE_HOME=/cache

# OUTPUT: Build artefacts (Wheels) are output here
VOLUME /wheelhouse

# OUTPUT: Test reports are output here
VOLUME /reports

# Add test entrypoint script
COPY scripts/test.sh /usr/local/bin/test.sh
RUN chmod +x /usr/local/bin/test.sh

ENTRYPOINT [ "test.sh" ]
CMD ["python", "manage.py", "test", "--noinput"]

# add application source
COPY src /application
WORKDIR /application