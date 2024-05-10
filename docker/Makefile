include .env

up:
	cp .env ../app/.env
	docker-compose up -d --build
	docker-compose exec php8 composer install
	docker-compose exec php8 bin/console doctrine:database:create --if-not-exists
	docker-compose exec php8 bin/console doctrine:migrations:migrate --no-interaction

down:
	docker-compose down -d

shell:
	docker-compose run php8 bash

database:
	docker-compose exec mysql5 mysql -uroot -p$(DATABASE_PASSWORD)

