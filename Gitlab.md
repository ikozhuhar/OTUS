:white_check_mark: _Задача: <a name='1'>Как выполнить push в ветку main (192.168.6.40) из удаленного Git</a>_  

```ruby
# создать локальный репозиторий
1. git clone https://gitlab.mosinzhproekt.ru/root/vendorportal.git
2. cd vendorportal
3. echo "Новый контент" > file.txt
4. git add . | git add file.txt
5. git commit -m "Ваше сообщение коммита"
6. git push origin main

Важные моменты:
	Без изменений push не сработает - нечего отправлять
	Обязательно нужны git add и git commit перед push

Дополнительные проверки которые можно добавить:
	# После клонирования проверить статус
	git status

	# После git add проверить что файлы добавлены
	git status

	# После коммита проверить историю
	git log --oneline -3


PS:

Настройка доступа для push:

Способ 1: Использование Personal Access Token (рекомендуется)

Создайте Personal Access Token в GitLab:
Зайдите в GitLab → Settings → Access Tokens
Название: "Server Access"
Срок действия: по вашему выбору
Scope: отметьте api и write_repository

Используйте токен как пароль:

git clone https://gitlab.mosinzhproekt.ru/root/vendorportal.git
# Логин: ваш_username
# Пароль: ваш_token


Способ 2: Настройка SSH ключей (более безопасно)

Создайте SSH ключ на сервере:

ssh-keygen -t ed25519 -C "your_email@example.com"
# Нажмите Enter для всех вопросов
Покажите публичный ключ:


cat ~/.ssh/id_ed25519.pub
Добавьте ключ в GitLab:

Settings → SSH Keys

Вставьте содержимое публичного ключа

Клонируйте через SSH:

git clone git@gitlab.mosinzhproekt.ru:root/vendorportal.git
```


<br>

:white_check_mark: _Задача: <a name='1'>На стороне внешнего gitlab (192.168.6.61)</a>_ 

```ruby
1. # Вход в контейнре gitlab
sudo docker exec -it gitlab bash

2. # Вход в интерактивную консоль Ruby
gitlab-rails console

3. # Список всех проектов
Project.all.each { |p| puts "#{p.id}: #{p.name}" }

projects = Project.all
projects.each do |project|
  puts "ID: #{project.id}, Name: #{project.name}"
end

Project.all.map { |p| "#{p.id}: #{p.name}" }

4. # Посчитаем проекты
Project.count

5. # Смотрим подробности по id 1
project = Project.find(1)
puts "ID: #{project.id}"
puts "Name: #{project.name}"
puts "Full path: #{project.full_path}"
puts "Namespace: #{project.namespace.full_path}"

6. # Смотрим все ветки во всех проектах
Project.all.each do |project|
  puts "=== #{project.name} ==="
  begin
    # Получаем ветки через repository
    branches = project.repository.branches
    branches.each { |branch| puts "  #{branch.name}" }
    puts "  Всего веток: #{branches.size}"
  rescue => e
    puts "  Ошибка: #{e.message}"
  end
  puts ""
end


7. Как посмотреть ветки только в CPBUP-ELO

# Получить просто массив имен веток
project = Project.find_by(name: "CPBUP-ELO")
branch_names = project.repository.branches.map(&:name)
puts branch_names

# Вариаты с деталями
project = Project.find_by(name: "CPBUP-ELO")
project.repository.branches.each do |branch|
  puts "🌿 #{branch.name}"
end

project = Project.find_by(name: "CPBUP-ELO")
project.repository.branches.each { |b| puts b.name }
```

<img width="1402" height="423" alt="image" src="https://github.com/user-attachments/assets/2ab66fe8-14bd-46a5-99ea-f88a386ddad8" />

<img width="1537" height="163" alt="image" src="https://github.com/user-attachments/assets/5833a332-3fa5-40b9-9f51-6eaecbb0867d" />

<img width="1528" height="120" alt="image" src="https://github.com/user-attachments/assets/70df799b-f532-4639-b9df-5df7d1a59146" />

<img width="1482" height="218" alt="image" src="https://github.com/user-attachments/assets/1ff10549-1e4c-473e-a72c-f55c0365720c" />



<br>

:white_check_mark: _Задача: <a name='1'>Последовательность для pull на стороне сервера 192.168.160.57</a>_ 

```ruby
sudo apt install git -y
git config --global user.name "ikozhuhar"
git config --global user.email "iuh77@mail.ru"
git config --global credential.helper cache
git config --global http.sslVerify false
git config --list
which git
git --version

# 1. Клонирование репозитория (если его еще нет)
git clone https://gitlab.mosinzhproekt.ru/root/vendorportal.git
cd vendorportal
git branch          # покажет ветки
git status          # покажет статус
git log --oneline   # покажет историю коммитов


# 2. Проверка подключения
git remote -v

# Должно показать:
origin  https://gitlab.mosinzhproekt.ru/root/vendorportal.git (fetch)
origin  https://gitlab.mosinzhproekt.ru/root/vendorportal.git (push)

# 3. Выполнение pull
git pull origin main


Важные моменты:

Клонирование нужно только один раз для первоначальной настройки
Последующие обновления делаются через git pull
Локальные изменения могут конфликтовать с удаленными - нужно решать конфликты

Проверка что всё работает:
# После клонирования/pull посмотреть файлы
ls -la

# Посмотреть историю коммитов
git log --oneline -5

# Посмотреть статус
git status
```

<img width="1500" height="361" alt="image" src="https://github.com/user-attachments/assets/4da597f8-df51-49e4-b94e-d1eed156abd5" />

<img width="1493" height="241" alt="image" src="https://github.com/user-attachments/assets/5d58909f-aa71-4c18-8965-641b146a5b34" />

<img width="1493" height="119" alt="image" src="https://github.com/user-attachments/assets/68ee6c55-26ba-474e-bfb9-890327c9a1a1" />

<img width="1498" height="170" alt="image" src="https://github.com/user-attachments/assets/d15b6ccb-7467-438f-8e99-1f88aa2d0e94" />


