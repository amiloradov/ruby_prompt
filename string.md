# **СТРОКИ**

## **Создаём строки**

**Создание строки:**

```ruby
title = ""							 # => ""
```
  ---

**Проверить пустая ли строка:**

```ruby
title.empty? 						# => true
```
  ---

**Проверить длину строки:**

```ruby
title.length
```
или
```ruby
title.size 							# => 0
```
  ---

## **Строки с общим ограничителем**

Строка вкладывается между парой парой символов-ограничителей, которым предшествует символ %:

```ruby
comedy = %!As you like it!

history = %[Henry 5]

tregedy = %(Julius Ceasar)
```

%Q является эквивалентом строки в двойных кавычках; %q — эквивалент одинарных кавычек; %x используется для строки в обратных кавычках ( ` ) при выводе команды.

## **Конкатенация строк**

Соседние строки могут быть сцеплены просто потому, что они стоят друг за другом:

```ruby
"Hello, " " " "World" "!" 			# => "Hello, World!"
```

Можно также воспользоваться методом +:

```ruby
"Hello, " + " " + "World" + "!" 	# => "Hello, World!"
```

Ещё один способ состоит в применение метода <<:

```ruby
"Hello, " << "World!" 				# => "Hello, World!"
```

Или соединить строки вместе, несколько раз вызвав <<:

```ruby
"Hello, " << "World" <<  "!" 		# => "Hello, World!"
```

Альтернативой << является метод concat (это метод не позволяет формировать цепочку):

```ruby
"Hello, ".concate "World!" 			# => "Hello, World!"
```

Можно сделать строку неизменной (заморозить её):

```ruby
greet = "Hello, World!"

greet.freeze
```

Проверить заморожен ли строка:

```ruby
greet.frozen? 						# => true
```
  ---

## **Получаем доступ к строкам**

```ruby
line = "A horse! A horse! my kindom for a horse!"

cite = "Akt 5, Scene 4"

speaker = "King Richard 3"
```
  
Если ввести к методу [] строку в качестве параметра, то он вернет эту строку если найдет:

```ruby
speaker['King'] 					# => "King"
```

Можно найти символ по индексу:

```ruby
line[7] 							# => "!"
```

Можно задать смещение и длину, чтобы сообщить позицию, с которой вы хотите начать, и сколько символов вы хотите извлечь:

```ruby
line[18, 23] 						# => "my kindom for a horse!"
```

Введите диапазон, чтобы указать диапазон символов:

```ruby
cite[0..4] 							# => "Act 5"

cite[0...4] 						# => "Act "
```

Метод **index** возвращает индекс:

```ruby
line.index("k") 					# => 21
```
  ---

## **Сравниваем строки**

```ruby
hay = "Four score and seven years ago our fathers brought forth, upon this continent, a new nation, conceived in Liberty, and dedicated to the propodition that all men are created equal. "

nicolay = "Four score and seven years ago our fathers brought forth, upon this continent, a new nation, conceived in liberty, and dedicated to the propodition that \"all men are created equal\ "
```
 
Сравним эти строки:

```ruby
hay == nicolay 						# => false
```

Можно также применить метод **eql?** И получить тот же результат, несмотря на то, что eql? и == слегка различны:

* == возвращает true, если равны два объекта String, и false в противном случае.

* eql? возвращает true, если две строки равны по длине и содержимому, и false в противном случае.

```ruby
hay.eql? nicolay 					# => false
```

Еще одно средство сравнения строк — это метод <=> (космический челнок). Он сравнивает значения кодов символов строки и возвращает -1 (меньше), 0 (равны), 1 (больше):

```ruby
"a" <=> "a" 						# => 0

"a" <=> "b" 						# => -1

"a" <=> "A" 						# => 1
```

Сравнить **без** учета регистра:

```ruby
"a".casecmp "A" 					# => 0
```
---

## **Вставляем строку в строку**

Метод **insert** позволяет вставить одну строку по указанному индексу в другую:

```ruby
"Be carful.".insert(6, "e")			# => "Be careful."
```
или добавить слово:
```ruby
"Be carуful.".insert(3, "very")		# => "Be very careful."
```
---

## **Заменяем всю строку или ее часть**

```ruby
line = "A Porsche! A Porsche! my kindom for a Porsche!"

cite = "Akt 5, Scene 5"

speaker = "King Richard, 2007"
```

Введите строку как параметр для []=, и он, если найдет ее, вернет новую, откорректированную строку:

```ruby
speaker[", 2007"]= " 3" 			# => "3"

p speaker 							# => "King Richard 3"
```

Можно ввести индекс:

```ruby
cite[13]= "4" 						# => "4"

p cite 								# => "Akt 5, Scene 4"
```

Можно указать смещение и длину:

```ruby
line[38, 8]= "Porsche 911 Turbo!" 	# => "Porsche 911 Turbo!"

p line 						# => "A Porsche! A Porsche! my kindom for a Porsche 911 Turbo!"
```
  
Можно ввести диапазон:

```ruby
speaker[12..17]= " the Third" 		# => "the Third"

p speaker 							# => "King Richard the Third"
```
  ---

## **Метод delete**

С помощью **delete** и **delete!** можно удалить символы в строке:

```ruby
"That“s call folks!".delete "c" 	# => "That“s all folks!"

"That“s calll folks!".delete "l" 	# => "That“s a foks!"
```

Можно отвергнуть весь параметр или его часть с помощью знака (^):

```ruby
"That“s all folks".delete "abcdefghijklmnopqrstuvwxyz", "^ha" # => "ha"
```
---

## **Заменяем подстроку**

Метод **gsub** замещает подстроку(первый параметр) замещающей строкой (второй параметр):

```ruby
"That“s calll folks!".gsub("alll", "all")	 # => "That“s all folks!"
```

Метод **replace** замещает строку целиком:

```ruby
call = "All hand on deck!"

call.replace "All feet on deck!" 			# => "All feet on deck!"
```
  ---

## **Перевернуть строку**

Это можно проделать с помощью метода **reverse**:

```ruby
"abcdefghijklmnopqrstuvwxyz".reverse 		# => "zyxwvusrqponmlkjihgfedcba"
```
 --- 

## **Из строки в массив**  

Метод **split** преобразует строку в массив:

```ruby
"0123456789".split 							# => ["0123456789"]
```

Можем указать параметр:

```ruby
"0123456789".split("") 				# => ["0", "1", "2", "3", "4", "5", "6", "7", "8", "9"]

c_w = "George Jones, Conway Twitty, Lefty Frizzell, Ferlin Husky"

c_w.split(", ") 	# => ["George Jones", "Conway Twitty", "Lefty Frizzell", "Ferlin Husky"]
```
  ---

## **Выполняем итерации в строке**

Метод **each_char** выполняет итерацию над каждым символом:

```ruby
"news".each_char{|item| print item, "/"} 					# => n/e/w/s/
```
  ---

## **downcase, upcase, capitalize и swapcase**

Метод **downcase** преобразует все символы строки в нижний регистр:

```ruby
"LITTLE".downcase 						# => "little"
```

Метод **upcase** преобразует все символы строки в верхний регистр:

```ruby
"big".upcase 							# => "BIG"
```

Метод **capitalize** преобразует первый символ строки в верхний регистр:

```ruby
"word".capitalize 						# => "Word"
```

Метод **swapcase** преобразует символы с верхним регистром в символы с нижним регистром и наоборот:

```ruby
"hAhAhA".swapcase 						# => "HaHaHa"
```
  ---

## **Преобразуем строки**

Можно преобразовать строку в число с плавающей точкой (Float) или целое число (Fixnum):

```ruby
"200".to_f 								# => 200.0

"100".to_i 								# => 100
```

Чтобы преобразовать строку в символ (Symbol):

```ruby
"name".to_sym 							# => :name
```
---
