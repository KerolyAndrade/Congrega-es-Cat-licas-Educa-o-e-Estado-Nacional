# Use uma imagem base do PHP com suporte ao Laravel
FROM php:8.2-fpm

# Instalar extensões necessárias
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    libpq-dev \
    && docker-php-ext-install pdo pdo_pgsql

# Instalar Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Instalar o Supervisor para gerenciar o processo do PHP-FPM
RUN apt-get install -y supervisor

# Configurar diretório de trabalho
WORKDIR /workspace

# Copiar os arquivos do projeto (ajustado para usar o .dockerignore)
COPY . .

# Criar as pastas storage e bootstrap/cache caso não existam
RUN mkdir -p /workspace/storage /workspace/bootstrap/cache

# Configurar permissões (ajustado para evitar conflitos com Codespaces)
RUN chown -R www-data:www-data /workspace \
    && chmod -R 775 /workspace/storage /workspace/bootstrap/cache

# Expor a porta para o PHP-FPM
EXPOSE 9000

# Comando inicial
CMD ["php-fpm"]
