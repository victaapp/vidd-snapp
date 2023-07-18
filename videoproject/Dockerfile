FROM python:3.10.4-slim

# 1. Disable python process buffering
ENV PYTHONUNBUFFERD 1

# 2. Change working directory to /app/server
WORKDIR /app/server
ADD . /app/server

ARG DEV=false

## ImageMagicK Installation ##
RUN mkdir -p /tmp/distr && \
    cd /tmp/distr && \
    apt-get update -y && \
    apt install wget unzip -y && \
    wget https://download.imagemagick.org/ImageMagick/download/releases/ImageMagick-7.0.11-2.tar.xz && \
    apt-get install xz-utils && \
    tar xvf ImageMagick-7.0.11-2.tar.xz && \
    cd ImageMagick-7.0.11-2 && \
    apt-get install build-essential -y && \
    ./configure --enable-shared=yes --disable-static --without-perl && \
    make && \
    make install && \
    ldconfig /usr/local/lib && \
    cd /tmp && \
    rm -rf distr

# ## Installing External Fonts ##
# RUN mkdir -p /usr/share/fonts/truetype/custom \
#     && for fontname in \
#     'Mrs Saint Delafield' 'Arimo' 'Dosis'; \
#     do \
#       modified_fontname=$fontname//[ ]/_}; \
#       wget "https://fonts.google.com/download?family=$fontname" -O $modified_fontname.zip; \
#       mkdir -p /usr/share/fonts/truetype/custom; \
#       unzip $modified_fontname.zip -d /usr/share/fonts/truetype/custom; \
#       rm $modified_fontname.zip; \
#     done
# 3. Install MySQL and PostgreSQL dev tools
# RUN apt-get update && apt-get install gcc default-libmysqlclient-dev libpq-dev -y

RUN pip install --upgrade pip && pip install -r requirements.txt

CMD python manage.py runserver 0.0.0.0:8000



# RUN apt-get update && apt-get install -y \
#     imagemagick libmagickwand-dev --no-install-recommends \
#     && pecl install imagick \
#     && docker-php-ext-enable imagick
