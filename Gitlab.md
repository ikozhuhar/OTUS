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

# 8. Как выполнить push в ветку main из удаленного сервера гита 

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

```
