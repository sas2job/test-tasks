1) Есть массив
[1, 2, 12, 34, 35, 6, 0, 34, 122, 124, 789, 999, 33, 54, 763, 893]

a) напишите функцию, которая получает на вход исходный массив и возвращает 2
максимальных значения

```ruby
def two_max_int(array)
  result = [0, 0]
  max = 0
  predmax = 0
  for i in 0..array.size - 1
    if array[i] > max
      max = array[i]
    elsif array[i] < max && array[i] > predmax
      predmax = array[i]
    end
  end
  result[1] = predmax
  result[0] = max
  result
end
```

```console
p two_max_int([1, 2, 12, 34, 35, 6, 0, 34, 122, 124, 789, 999, 33, 54, 763, 893])

# => [999, 893]
```

b) напишите функцию, которая получает на вход исходный массив и возвращает 2 минимальных значения

```ruby
def two_min_short(array)
  array.min(2)
end
```

```console
p two_min_short([1, 2, 12, 34, 35, 6, 0, 34, 122, 124, 789, 999, 33, 54, 763, 893])

# => [0, 1]
```

2) Есть массив
arr = [{a: 1, b: 2, c: 45}, {d: 123, c: 12}, {e: 87}]

a) напишите выражение, которое получает массив всех ключей

```ruby
def array_of_keys(arr)
  arr.map(&:keys).flatten
end
```

```console
p array_of_keys([{a: 1, b: 2, c: 45}, {d: 123, c: 12}, {e: 87}])
=> [:a, :b, :c, :d, :c, :e]
```

# b) напишите выражение, которое получает массив всех значений

```ruby
def array_of_values(arr)
  arr.map(&:values).flatten
end
```

```console
p array_of_values([{a: 1, b: 2, c: 45}, {d: 123, c: 12}, {e: 87}])

=> [1, 2, 45, 123, 12, 87]
```

с) напишите выражение, которое получает сумму всех значений

```ruby
def array_of_sum_values(array)
  array.map(&:values).flatten.inject(:+)
end
```

```console
p array_of_sum_values([{a: 1, b: 2, c: 45}, {d: 123, c: 12}, {e: 87}])

=> 270
```

3) Найдите вхождения каждого элемента в массив
[ nil, 2, :foo, "bar", "foo", "apple", "orange", :orange, 45, nil, :foo, :bar, 25, 45, :apple, "bar", nil]
чтобы на выходе получился Hash по типу { элемент => количество вхождений в массив}

```ruby
def count_for_element(arr)
  arr.inject(Hash.new(0)){|hash, count| hash[count] += 1; hash}
end
```

```console
p count_for_element([ nil, 2, :foo, "bar", "foo", "apple", "orange", :orange, 45, nil, :foo, :bar, 25, 45, :apple, "bar", nil])

=> {nil=>3, 2=>1, :foo=>2, "bar"=>2, "foo"=>1, "apple"=>1, "orange"=>1, :orange=>1, 45=>2, :bar=>1, 25=>1, :apple=>1}
```

4) Напишите функцию
a) которая переводит градусы по Цельсию в градусы по Фаренгейту (формулу нужно
найти в интернете)

```ruby
def convert(c)
  (c*9/5)+32
end
```

```console
p convert(10)

=> 50
```

b) напишите консольную программу, которая просит юзера ввести число (градусы по
Цельсию) и переводит его в Фаренгейты

```ruby
def convert(c)
  (c*9/5)+32
end

puts "Введите число(градусы по Цельсию): "

number = gets.to_i
puts convert(number)
```

```console
Введите число(градусы по Цельсию):
-> 25
=> 77
```

с) необязательно, но будет плюсом Напишите обработку ошибок, если юзер ввел
неправильные данные (программа должна просить ввести число заново и сообщать об
ошибке, но не прерываться)

```ruby
def convert(c)
  (c*9/5)+32
end

loop do
  puts "Введите число(градусы по Цельсию): "

  input_string = gets.chomp

  begin
    temp = Integer(input_string)
    puts "#{convert(input_string.to_i)} градусов по Фаренгейту"
    break
  rescue
    puts "#{input_string} не является числом."
  end
end
```

```console
Введите число(градусы по Цельсию): 
-> kk
=> kk не является числом.
Введите число(градусы по Цельсию): 
Введите число(градусы по Цельсию): 
-> 30
=> 86 градусов по Фаренгейту
```

5) Напишите функцию, которая имитирует работу светафора
a) на вход она получает один из цветов в виде строки (‘red’, ‘green’, ‘yellow’ ), на выходе
будет результат (идти, стоять или ждать)
b) напишите это в виде консольной программы, которая не прекращает работу после
однократного вызова, а ждет следующих запросов

traffic light = {"red": "стоять", "green": "идти", "yellow": "ждать"}

```ruby
traffic_light = {"red": "стоять", "green": "идти", "yellow": "ждать"}

loop do
  puts "Введите цвет сфетофора(red/green/yellow): "

  input_string = gets.chomp.to_sym

  # p traffic_light.any?{|input_string| traffic_light.key?(input_string)} 
  
  if traffic_light.keys.include?(input_string)
    puts "#{traffic_light[input_string]}" 
  else
    puts "Неверное значение, повторите еще раз."
  end
  puts
end
```

```console
Введите цвет сфетофора(red/green/yellow): 
-> test
=> Неверное значение, повторите еще раз.

Введите цвет сфетофора(red/green/yellow): 
-> green
=> идти
```

c) необязательно, но будет плюсом напишите обработку некорректных данных и
добавьте возможность юзеру завершить работу программы

```ruby
traffic_light = {"red": "стоять", "green": "идти", "yellow": "ждать"}

loop do
  puts "Введите цвет сфетофора(red/green/yellow): "
  puts "Для выхода нажмите Enter"

  input_string = gets.chomp
    if input_string == ""
      exit
    else
      value = input_string.to_sym
      if traffic_light.keys.include?(value)
        puts "#{traffic_light[value]}" 
      else
        puts "Неверное значение, повторите еще раз."
      end
    puts
    end
end
```

```console
Введите цвет сфетофора(red/green/yellow): 
Для выхода нажмите Enter
-> test
=> Неверное значение, повторите еще раз.

Введите цвет сфетофора(red/green/yellow): 
Для выхода нажмите Enter
-> red
=> стоять

Введите цвет сфетофора(red/green/yellow): 
Для выхода нажмите Enter

```

5) Обязательное задание
Есть таблица students с колонками
id int
name varchar
created_at datetime
parent_id int
a) посчитайте количество всех студентов
b) посчитайте количество студентов с именем Иван
c) посчитайте количество студентов созданных после 1 сентября 2020 года

7) Необязательная, но выполнение будет очень большим плюсом
a)Напишите простой блог на рельсе с минимальным функционалом (один автор,
который выкладывает посты. Комментарии, сортировки, фильтры и основные рюшечки
не обязательны, но остаются на ваше усмотрение и желание. Как и стилизация)

[Github](https://github.com/sas2job/blog) - репозиторий на Github

b) выложить проект на Heroku

[Heroku](https://infinite-brook-79881.herokuapp.com/) - репозиторий на Heroku