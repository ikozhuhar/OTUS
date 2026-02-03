### Создание собственного/служебного репозитория Astra 1.8

✅ _Вариант 1: Простое зеркало_

```ruby
1. sudo apt update && sudo apt dist-upgrade
2. sudo apt install apt-mirror apache2
3. sudo mkdir -p /var/repo/astra1.8-mirror
4. sudo chown apt-mirror:www-data /var/repo/astra-mirror       # Права
5. sudo -u apt-mirror apt-mirror                               # Синхронизация
6. sudo ln -s /var/repo/astra1.8-mirror /var/www/html/astra1.8 # Симлинк на зеркало
7. Настройка Apache
8. sudo systemctl restart apache2

9. На клиентах в /etc/apt/sources.list:
deb http://repos.mip.ru/astra1.8/mirror/download.astralinux.ru/astra/stable/1.8_x86-64/repository-extended/ 1.8_x86-64 main contrib non-free non-free-firmware
deb http://repos.mip.ru/astra1.8/mirror/download.astralinux.ru/astra/stable/1.8_x86-64/repository-main/ 1.8_x86-64 main contrib non-free non-free-firmware

ОБНОВЛЕНИЕ

# 1. Синхронизация
sudo -u apt-mirror apt-mirror

https://dzen.ru/a/ZMoCvaLDAklOFRZj
```

<img width="1333" height="267" alt="image" src="https://github.com/user-attachments/assets/b1f91f8c-59d2-4297-a1c9-4011f5ea7451" />
<img width="1452" height="403" alt="image" src="https://github.com/user-attachments/assets/ff966a60-418c-4c37-af5b-927f752404d2" />


<br><br>

✅ _Вариант 2: Reprepro (для управления пакетами)_

```ruby
1. sudo apt update && sudo apt dist-upgrade
2. sudo apt install apt-mirror reprepro apache2
3. sudo mkdir -p /var/repo/astra1.8-mirror
4. sudo chown apt-mirror:www-data /var/repo/astra1.8-mirror    # Права
5. sudo -u apt-mirror apt-mirror                               # Синхронизация
6. sudo mkdir -p /var/repo/astra1.8/conf                       # Репозиторий
7. sudo nano /var/www/html/astra1.8/conf/distributions         # Файл distributions
8. sudo reprepro -b /var/repo/astra1.8 clearvanished           # Очистки ранее созданной базы
9. sudo reprepro -b /var/repo/astra1.8 export                  # Инициализации нового репозитория
10. sudo find /var/repo/astra1.8-mirror/mirror/download.astralinux.ru/astra/stable/1.8_x86-64/repository-main/pool -name "*.deb" -exec reprepro -b /var/repo/astra1.8 includedeb 1.8_x86-64 {} \;
11. sudo find /var/repo/astra1.8-mirror/mirror/download.astralinux.ru/astra/stable/1.8_x86-64/repository-extended/pool -name "*.deb" -exec reprepro -b /var/repo/astra1.8 includedeb 1.8_x86-64 {} \;
12. sudo ln -s /var/repo/astra1.8 /var/www/html/astra1.8

13. На клиентах в /etc/apt/sources.list:
deb [trusted=yes] http://repos.mip.ru/astra1.8/mirror/download.astralinux.ru/astra/stable/1.8_x86-64/repository-extended/ 1.8_x86-64 main contrib non-free non-free-firmware
deb [trusted=yes] http://repos.mip.ru/astra1.8/mirror/download.astralinux.ru/astra/stable/1.8_x86-64/repository-main/ 1.8_x86-64 main contrib non-free non-free-firmware


ОБНОВЛЕНИЕ: Полная пересборка (самый чистый)

# Останавливаем веб-сервер на время обновления
sudo systemctl stop apache2

# Полное зеркалирование
sudo -u apt-mirror apt-mirror

# УДАЛЯЕМ старый репозиторий и создаем новый
sudo rm -rf /var/repo/astra1.8
sudo mkdir -p /var/repo/astra1.8/conf
# ... создаем distributions файл ...
sudo reprepro -b /var/repo/astra1.8 export

# Добавляем пакеты
sudo find /var/repo/astra1.8-mirror/mirror/download.astralinux.ru/astra/stable/1.8_x86-64/repository-main/pool -name "*.deb" -exec reprepro -b /var/repo/astra1.8 includedeb 1.8_x86-64 {} \;
sudo find /var/repo/astra1.8-mirror/mirror/download.astralinux.ru/astra/stable/1.8_x86-64/repository-extended/pool -name "*.deb" -exec reprepro -b /var/repo/astra1.8 includedeb 1.8_x86-64 {} \;

# Запускаем веб-сервер
sudo systemctl start apache2

https://wiki.astralinux.ru/pages/viewpage.action?pageId=3277393
```

<img width="1359" height="225" alt="image" src="https://github.com/user-attachments/assets/7fa09627-72cc-46a9-91a0-2146889be41d" />


<br><br>

✅ _TROUBLESHOOTING_

```ruby
sudo find /var/repo/debian12-mirror -name "*.gz" -o -name "Release" -o -name "Packages" | head -10
```

```ruby
padmin@astra-17:/var$ sudo apt update
Игн:1 http://repos.mip.ru/astra17/mirror/dl.astralinux.ru/astra/stable/1.7_x86-64/repository-main 1.7_x86-64 InRelease
Игн:2 http://repos.mip.ru/astra17/mirror/dl.astralinux.ru/astra/stable/1.7_x86-64/repository-update 1.7_x86-64 InRelease
Игн:3 http://repos.mip.ru/astra17/mirror/dl.astralinux.ru/astra/stable/1.7_x86-64/repository-base 1.7_x86-64 InRelease
Игн:4 http://repos.mip.ru/astra17/mirror/dl.astralinux.ru/astra/stable/1.7_x86-64/repository-extended 1.7_x86-64 InRelease
Ошб:5 http://repos.mip.ru/astra17/mirror/dl.astralinux.ru/astra/stable/1.7_x86-64/repository-main 1.7_x86-64 Release
  404  Not Found [IP: 192.168.13.37 80]
Ошб:6 http://repos.mip.ru/astra17/mirror/dl.astralinux.ru/astra/stable/1.7_x86-64/repository-update 1.7_x86-64 Release
  404  Not Found [IP: 192.168.13.37 80]
Ошб:7 http://repos.mip.ru/astra17/mirror/dl.astralinux.ru/astra/stable/1.7_x86-64/repository-base 1.7_x86-64 Release
  404  Not Found [IP: 192.168.13.37 80]
Ошб:8 http://repos.mip.ru/astra17/mirror/dl.astralinux.ru/astra/stable/1.7_x86-64/repository-extended 1.7_x86-64 Release
  404  Not Found [IP: 192.168.13.37 80]
Чтение списков пакетов… Готово
E: Репозиторий «http://repos.mip.ru/astra17/mirror/dl.astralinux.ru/astra/stable/1.7_x86-64/repository-main 1.7_x86-64 Release» не содержит файла Release.
N: Обновление из этого репозитория нельзя выполнить безопасным способом, поэтому по умолчанию он отключён.
N: Информацию о создании репозитория и настройках пользователя смотрите в справочной странице apt-secure(8).
E: Репозиторий «http://repos.mip.ru/astra17/mirror/dl.astralinux.ru/astra/stable/1.7_x86-64/repository-update 1.7_x86-64 Release» не содержит файла Release.
N: Обновление из этого репозитория нельзя выполнить безопасным способом, поэтому по умолчанию он отключён.
N: Информацию о создании репозитория и настройках пользователя смотрите в справочной странице apt-secure(8).
E: Репозиторий «http://repos.mip.ru/astra17/mirror/dl.astralinux.ru/astra/stable/1.7_x86-64/repository-base 1.7_x86-64 Release» не содержит файла Release.
N: Обновление из этого репозитория нельзя выполнить безопасным способом, поэтому по умолчанию он отключён.
N: Информацию о создании репозитория и настройках пользователя смотрите в справочной странице apt-secure(8).
E: Репозиторий «http://repos.mip.ru/astra17/mirror/dl.astralinux.ru/astra/stable/1.7_x86-64/repository-extended 1.7_x86-64 Release» не содержит файла Release.
N: Обновление из этого репозитория нельзя выполнить безопасным способом, поэтому по умолчанию он отключён.
N: Информацию о создании репозитория и настройках пользователя смотрите в справочной странице apt-secure(8).


Проблема та же, что была с Debian: метаданные скачались в skel/, но НЕ были перемещены в финальную директорию mirror/ из-за сетевых ошибок при загрузке пакетов.

Решение: переместите метаданные вручную так как apt-mirror из-за ошибок загрузки пропустил финальный шаг
# 1. Создайте недостающую структуру директорий
sudo mkdir -p /var/repo/debian12-mirror/mirror/mirror.yandex.ru/debian/dists/

# 2. Переместите метаданные из skel в mirror (для основного репозитория)
sudo cp -r /var/repo/debian12-mirror/skel/mirror.yandex.ru/debian/dists/* /var/repo/debian12-mirror/mirror/mirror.yandex.ru/debian/dists/

# 3. Переместите метаданные для security (они уже успешно переместились, но на всякий случай)
sudo cp -r /var/repo/debian12-mirror/skel/mirror.yandex.ru/debian-security/dists/* /var/repo/debian12-mirror/mirror/mirror.yandex.ru/debian-security/dists/ 2>/dev/null || echo "Security уже перемещены"

# 4. Проверьте структуру
ls -la /var/repo/debian12-mirror/mirror/mirror.yandex.ru/debian/dists/



# Быстрая проверка работоспособности

# 1. Проверьте наличие ключевых файлов
ls -la /var/repo/debian12-mirror/mirror/mirror.yandex.ru/debian/dists/bookworm/Release

# 2. Проверьте доступность через веб
curl -I http://localhost/debian12/mirror/mirror.yandex.ru/debian/dists/bookworm/Release

# 3. Проверьте весь путь
curl http://localhost/debian12/mirror/mirror.yandex.ru/debian/dists/bookworm/ | head -20

# Проверьте основной репозиторий
curl -I http://localhost/astra17/mirror/dl.astralinux.ru/astra/stable/1.7_x86-64/repository-main/dists/1.7_x86-64/Release

# Проверьте другие репозитории
curl -I http://localhost/astra17/mirror/dl.astralinux.ru/astra/stable/1.7_x86-64/repository-update/dists/1.7_x86-64/Release
```

