# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.145.0/containers/ubuntu/.devcontainer/base.Dockerfile

# [Choice] Ubuntu version: bionic, focal
ARG VARIANT="focal"
FROM mcr.microsoft.com/vscode/devcontainers/base:0-${VARIANT}

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
     && apt-get -y install --no-install-recommends php php-xml php-mbstring php-intl php-curl php-zip vim

#RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
#     && php -r "if (hash_file('sha384', 'composer-setup.php') === '795f976fe0ebd8b75f26a6dd68f78fd3453ce79f32ecb33e7fd087d39bfeb978342fb73ac986cd4f54edd0dc902601dc') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
#     && php composer-setup.php \
#     && php -r "unlink('composer-setup.php');" \
#     && mv composer.phar /usr/local/bin/composer

# Install composer
RUN curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer

# Install symfony
RUN wget https://get.symfony.com/cli/installer -O - | bash && mv /root/.symfony/bin/symfony /usr/local/bin/symfony

# speedup with hirak/prestissimo
RUN composer config --global repositories.packagist composer https://packagist.jp
RUN composer global require hirak/prestissimo

CMD cd /workspaces/symfony-docker-vscode && /usr/local/bin/composer install