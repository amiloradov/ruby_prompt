# **МАССИВЫ**

Любой объект, который создает Ruby, может храниться в массиве. Любой элемент в массиве связан с индексом (index), и к нему можно обращаться по индексу.

Элементы массива автоматически проиндексированы, начиная с 0.

## **Создаем массив**

```ruby
month = [nil, "January", "February", "Match", "April", "May", "June", "July", "August", "September", "October", "November", "December"]
```
 
### **Создаем массив с помощью блока**

```ruby
num = Array.new(10) { |e| e = e*2 }		 # => [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
```
  
### **Создаем массив с помощью диапазона**

```ruby
digits = Array(0..9)					 # => [1, 2, 3, 4, 5, 6, 7, 8, 9]
```
  
## **Получаем доступ к элементам массива**

```ruby
q1 = ["January", "February", "Match"]
```
 
Получить доступ к первому элементу массива:

```ruby
q1[0]				 # => January
```
или
```ruby
q1.first			 # => January
```
  
Получить доступ к последнему элементу массива:

```ruby
q1[-1]				 # => March
```
или
```ruby
q1.last				 # => March
```
  
Методы **first**, **last** могут принимать целочисленные параметры, указывающие на количество элементов, которые необходимо возвратить:

```ruby
q1.first 2			 # => ["January", "February"]

q1.last 1			 # => ["Match"]
```
  
Возвратить индекс элемента:

```ruby
q1.index "Match"	 # => 2
```

Подобным образом, **rindex** отбирает последний элемент, соответствующий объекту.

Для демонстрации следующих методов возьмем массив:

```ruby
year = [2000, 2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009]
```
  
Можно указать, откуда начинать отсчитывать элементы и сколько элементов вы хотите:

```ruby
year[0, 3]			 # => [2000, 2001, 2002]
```
 
Можно также использовать диапазон:

```ruby
year[7..9]			 # => [2007, 2008, 2009]
```

Вместо [ ] можно применять метод **slice**:

```ruby
year.slice(1)		 # => 2001

year.slice(0, 4)	 # => [2000, 2001, 2002, 2003]

year.slice(0..2)	 # => [2000, 2001, 2002]

year.slice(0...2)	 # => [2000, 2001]
```
  
Метод **include?** проверяет, включает ли массив элемент с заданным значением:

```ruby
year.include? 2004		 # => true

year.include? (2010)	 # => false
```
---

## **Конкатенация**

Создадим несколько массивов:

```ruby
q1 = ["January", "February", "Match"]

q2 = ["April", "May", "June"]

q3 = ["July", "August", "September"]

q4 = ["October", "November", "December"]
```
  
Соединим эти массивы при помощи +:

```ruby
half1 = q1 + q2

half2 = q3 + q4

yr = half1 + half2
```
  
Аналогично методу + можно подцепить один массив к другому методом **concat**:

```ruby
last_part = q3.concat(q4)
```
  
Можно образовать цепочку методом <<:

```ruby
yrs = [1999]

yrs << 2000 << 2001 << 2002
```
---

## **Операции над множествами**

Ruby может выполнять такие операции над множествами, как:

* пересечение с помощью &

* разность с помощью -

* объединение с помощью |

Пересечение создает новый массив, объединяя общие элементы двух массивов и удаляя разные элементы и дубликаты:

```ruby
tue = ["shop", "make pie", "sleep"]

wed = ["shop", "make pie", "read", "sleep"]

tue & wed									 # => ["shop", "make pie", "sleep"]
```
  
Разность создает новый массив, объединяя общие элементы двух массивов и удаляя разные элементы и дубликаты:

```ruby
wed — tue				 # => ["read"]
```
  
Объединение ( | ) соединяет два массива вместе, удаляя дубликаты:

```ruby
tue | wed				 # => ["shop", "make pie", "read", "sleep"]
```
  
Метод **uniq**, также удаляет дубликаты:

```ruby
shopping_list = ["cheese", "bread", "crackers", "potatoes", "carrots", "cheese"]

shopping_list.uniq!			 # => ["cheese", "bread", "crackers", "potatoes", "carrots"]
```
---

## **Методы push и pop**

```ruby
fruit = ["apple", "orange", "banana"]

fruit.pop			 # => "banana"

p fruit				 # => ["apple", "orange"]

fruit.push "mango"

p fruit				 # => ["apple", "orange", "mango"]
```
---

## **Сравниваем массивы**

Вот три метода, которые позволят сравнить массивы: **==**, **<=>** и **eql?**.

Метод == сравнивает два массива на равенство. Два массива считаются равными, если, во-первых, они содержат одно и то же количество элементов и, во-вторых, каждый элемент равен соответствующему элементу в другом массиве.

С методом == близко связан метод eql?. Разница в том, что eql? дополнительно проверяет, имеют ли значения один и тот же тип.

Когда оператор <=> сравнивает два массива, сравнение выполняется для каждого объекта в массивах. Два массива считаются равными, если они имеют одинаковую длину и если значение каждого элемента равно значению соответствующего элемента в другом массиве. Когда сравнение выполнено, оператор определяет, больше, меньше или равны друг другу значения сравниваемых элементов. Возвращает: -1 — для "меньше"; 0 — для "равно"; 1 — для "больше".

---
 
## **Изменяем элементы**

```ruby
month = ["nil", "January", "February", "Match", "April", "May", "June", "July", "August", "September", "October", "November", "December"]
```

Изменим строку "nil" на значение nil при помощи **insert**:

```ruby
month.insert(0, nil)	 # => [nil, "January", "February", "Match", "April", "May", "June", "July", "August", "September", "October", "November", "December"]
```
  
Изменим элементы с помощью диапазона:

```ruby
month[5..7] = "Mai", "Juni", "Juli"		 # => [nil, "January", "February", "Match", "April", "Mai", "Juni", "Juli", "August", "September", "October", "November", "December"]
```
 
Можно проделать то же самое при помощи параметров начала и длины:

```ruby
month[5, 3] = "May", "Juny", "July"		 # => [nil, "January", "February", "Match", "April", "May", "Juny", "July", "August", "September", "October", "November", "December"]
```
---

## **Из массива в строку**

С помощью **to_s** можно извлечь элементы массива как отдельные строки:

```ruby
greeting = ["Hello! ", "Bonjour! ", "Guten Tag!"]

puts greeting.to_s				 # => Hello! Bonjour! Guten Tag!
```

С помощью **join** можно сбить все элементы в единую строку или указать разделитель между ними:

```ruby
month.join			 # => "JanuaryFebruaryMatchAprilMayJuneJulyAugustSeptemberOctoberNovemberDecember"

month.join ", "		 # => "January, February, Match, April, May, June, July, August, September, October, November, December"
```
 ---
 
## **Методы shift и unshift**

Метод **shift** удаляет элемент в начале массива:

```ruby
dates = [4, 5, 6, 7]

dates.shift

p dates			 # => [5, 6, 7]
```
 
Метод **unshift** добавляет элемент в начало массива:

```ruby
dates.unshift 4			 # => [4, 5, 6, 7]

dates.unshift (2, 3)	 # => [2, 3, 4, 5, 6, 7]
```
---

## **Удаление элементов массива**

Метод **delete** удаляет соответствующий объект из массива:

```ruby
month_a = ["nil", "jan", "feb", "mar", "apr", "may", "jun", "jul", "aug", "sep", "oct", "nov", "des"]

month_a.delete("nil")			 # => ["jan", "feb", "mar", "apr", "may", "jun", "jul", "aug", "sep", "oct", "nov", "des"]
```

Этот метод может принимать блок. Если объект не найден, выполняется результат выполнения блока:

```ruby
month_a.delete("noon") {"noon was't found. What are you going to do about it?"}
```

С помощью **delete_at** можно удалить элемент на основе его индекса:

```ruby
month_a.delete_at(12)

p month_a				 # => ["nil", "jan", "feb", "mar", "apr", "may", "jun", "jul", "aug", "sep", "oct", "nov"]
```
---

## **Массивы и блоки**

Метод **each** позволяет перебрать все элементы в массиве. Приведенный далее вызов меняет month_a (без nil) первую букву на заглавную:

```ruby
month_a.each {|e| e.capitalize + " "}
```

Он вырабатывает строку, а не массив:

```ruby
"Jan Feb Mar Apr May Jun Jul Aug Sep Oct Nov Dec"
```

Метод map подобен each, но вместо строки он возвращает новый массив:

```ruby
month_a_2020 = month_a.map {|e| e.capitalize + " 2020"}

p month_a_2020			 # => ["Jan 2020", "Feb 2020", "Mar 2020", "Apr 2020", "May 2020", "Jun 2020", "Jul 2020", "Aug 2020", "Sep 2020", "Oct 2020", "Nov 2020", "Des 2020"]
```
---

## **Прямая и обратная сортировка**

```ruby
х = [2, 5, 1, 7, 23, 99, 14, 27]
```

Метод **sort** выстраивает элементы по порядку:

```ruby
х.sort!			 # => [1, 2, 5, 7, 14, 23, 27, 99]
```
  
Метод **reverse** изменяет порядок расположения элементов в массиве на обратный:

```ruby
х.reverse		 # => [99, 27, 23, 14, 7, 5, 2, 1]
```
---

## **Многомерные массивы**

Многомерный массив — это массив массивов. Например:

```ruby
d2 = [ ["January", 2020], ["February", 2020], ["March", 2020] ]
```

Превратим двумерный массив в одномерный с помощью метода **flatten**:

```ruby
d2.flatten			 # => [ "January", 2020, "February", 2020, "March", 2020 ]
```

Двумерный массив подобен таблице со строками и столбцами. Преобразуем d2 с помощью **transpose**:

```ruby
d2.transpose		 # => [ ["January", "February", "March"], [2020, 2020, 2020] ]
```
---
