# DRF API Learning Project

Bu loyiha Django REST Framework (DRF) ni o'rganish va mustahkamlash uchun yaratilgan. Loyihada turli API endpointlar, autentifikatsiya, background tasks va boshqa DRF xususiyatlari amalga oshirilgan.

## Texnologiyalar

- **Django 5.2** - Web framework
- **Django REST Framework 3.16.1** - API framework
- **PostgreSQL** - Database
- **Redis** - Cache va message broker
- **Celery** - Background tasklar
- **Celery Beat** - Scheduled tasklar
- **Flower** - Celery monitoring
- **Nginx** - Web server
- **Gunicorn** - WSGI server
- **Docker Compose** - Container orchestration
- **uv** - Python package manager

## O'rnatish

### Talablar

- Docker
- Docker Compose

### Ishga tushirish

1. Environment faylini nusxalash:
```bash
cp .env.example .env.prod
```

2. Docker compose bilan ishga tushirish:
```bash
docker compose up -d --build
```

3. Migratsiyalarni yuritish:
```bash
docker compose exec backend_service uv run python manage.py migrate
```

4. Static fayllarni yig'ish:
```bash
docker compose exec backend_service uv run python manage.py collectstatic --noinput
```

5. Superuser yaratish:
```bash
docker compose exec backend_service uv run python manage.py createsuperuser
```

API `http://localhost:8005` da ishlaydi.

## API Endpointlar

### Ochiq APIlar (Autentifikatsiyasiz)

- `GET /api/v1/regions/` - Viloyatlar ro'yxati
- `GET /api/v1/districts/` - Tumanlar ro'yxati
- `GET /api/v1/categories/` - Kategoriyalar ro'yxati
- `GET /api/v1/products/` - Mahsulotlar ro'yxati

### Autentifikatsiya talab qilinadigan APIlar

- `POST /api/v1/register/` - Ro'yxatdan o'tish (SMS kod yuboriladi)
- `POST /api/v1/login/` - Tizimga kirish
- `POST /api/v1/change-password/` - Parolni o'zgartirish
- `GET /api/v1/users/profile/` - Profil ma'lumotlari
- `PUT /api/v1/users/profile/` - Profilni yangilash
- `GET /api/v1/users/addresses/` - Manzillar ro'yxati
- `GET /api/v1/users/favorites/` - Sevimlilar ro'yxati
- `GET /api/v1/users/cart/` - Savat ro'yxati
- `PUT /api/v1/users/cart/{pk}/update/` - Savatni yangilash
- `DELETE /api/v1/users/cart/{pk}/delete/` - Savatdan o'chirish
- `POST /api/v1/users/cart/{pk}/add/` - Savatga qo'shish

## Xususiyatlar

### ✅ Amalga oshirilgan

1. **Region va District API** - Ochiq API sifatida ishlaydi
2. **User API** - GET methodi yopiq (faqat o'z ma'lumotlari)
3. **Category API** - Kategoriyalar uchun CRUD
4. **Product API** - Mahsulotlar uchun CRUD
5. **User Model** - Username maydoni olib tashlandi
6. **SMS yuborish** - Django background task orqali
7. **Change Password** - Parolni o'zgartirish
8. **Register** - Phone, code, random password (6 ta belgi) bilan ro'yxatdan o'tish
9. **Profile yangilash** - Profil ma'lumotlarini o'zgartirish
10. **Cart API** - Savat boshqaruvi
11. **Favorite API** - Sevimlilar boshqaruvi
12. **Address API** - Manzillar boshqaruvi (default address bilan)

### Autentifikatsiya

- JWT token (SimpleJWT)
- Access va Refresh tokenlar
- Token refresh endpoint

### Background Tasks

- Celery orqali SMS yuborish
- Celery Beat bilan scheduled tasks
- Flower orqali monitoring (http://localhost:5001/flower/)

### Filterlar

- django-filter orqali mahsulotlarni filterlash
- Region, district, category bo'yicha filter

## API Dokumentatsiyasi

API dokumentatsiyasi uchun drf-spectacular ishlatilgan. Swagger UI:
- `http://localhost:8005/api/schema/swagger-ui/`

## Database

PostgreSQL ishlatiladi. Docker container ichiga kirish:
```bash
docker exec -it postgres_service sh
su postgres
psql
```

## Development

Local development uchun:
```bash
# Virtual environment yaratish
python -m venv .venv
source .venv/bin/activate

# Dependencylarni o'rnatish
uv sync

# Migratsiyalar
uv run python manage.py migrate

# Server ishga tushirish
uv run python manage.py runserver
```

## Project Structure

```
drf_p35/
├── apps/               # Main app
│   ├── models/         # Model files
│   ├── serializers.py  # DRF serializers
│   ├── views.py        # API views
│   ├── urls.py         # URL routes
│   ├── filters.py      # Django filters
│   ├── tasks.py        # Celery tasks
│   └── fixtures/       # Test data
├── root/               # Django project settings
├── docker-compose.yaml # Docker services
├── Dockerfile          # Backend container
├── nginx.conf          # Nginx configuration
└── pyproject.toml      # Project dependencies
```

## O'rganilgan Konsepsiyalar

- Django REST Framework asoslari
- Serializers va ViewSets
- JWT autentifikatsiya
- Permissionlar va authentication
- Django filters
- Background tasks (Celery)
- Docker va Docker Compose
- Nginx reverse proxy
- API dokumentatsiyasi (drf-spectacular)
- Database migrations
- Model relationships (ForeignKey, ManyToMany)
- File upload (rasm yuklash)

## License

Bu loyiha o'rganish maqsadida yaratilgan.
