# **ХЭШИ**

**Хэш** — это неупорядоченная коллекция пар "ключ-значение", хэш подобен массиву, но вместо целочисленного индекса, индексирование производится по ключам, которые могут быть составлены из любых объектов Ruby.

## **Создаем хэш**

```ruby
month_a = { "jan" => "January", "feb" => "February", "mar" => "March", "apr" => "April", "may" => "May", "jun" => "June", "jul" => "July", "aug" => "August", "sep" => "September", "oct" => "October", "nov" => "November", "dec" => "December" }
```
---

## **Получаем доступ к хэшам**

```ruby
zip = { 82442 => "Ten Sleep", 83025 => "Teton Village", 83127 => "Thayne", 82443 => "Thermopolis", 82084 => "Tie Siding", 82336 => "Tipton", 82240 => "Turnerville", 83110 => "Torrington", 83112 => "Turnerville" }
```

Проверить есть заданный ключ в хэше можно с помощью: **key?**, **has_key?**, **member?** или **include?**:

```ruby
zip.has_key?		 # => true
```
  
Можно, наоборот, посмотреть имеется ли заданное значение, при помощи **value?** или **has_value?**:

```ruby
zip.has_value?		 # => true
```

Извлечь из хэша единичное значение по ключу:

```ruby
zip[82442]			 # => "Ten Sleep"
```
 
При помощи метода **keys** вернем массив, содержащий все ключи:

```ruby
zip.keys			 # => [83110, 83127, 82336, 83112, 82084, 83025, 82442, 82443, 82240]
```

При помощи метода **values** получим все значения, хранящиеся в хэше:

```ruby
zip.values			 # => { "Turnerville", "Thayne", "Tipton", "Turnerville", "Tie Siding", "Teton Village", "Ten Sleep", "Thermopolis", "Torrington" }
```

Извлечем из хэша значения на основе одного или нескольких ключей методом **values_at**:

```ruby
zip.values_at 82084			 # => ["Tie Siding"]

zip.values_at 82442, 82443, 82240			 # => ["Ten Sleep", "Thermopolis", "Torrington"]
```

Вернем значение ключа методом **index**:

```ruby
zip.index "Thayne"			 # => 83127
```
 
Метод **select** использует блок и возвращает новый , многомерный массив пар "ключ-значение":

```ruby
zip.select { |key, val| key > 83000 }			 # => [[83110, "Turnerville"], [83127, "Thayne"], [83112, "Turnerville"], [83025, "Teton Village"]]
```
---

## **Итерации**

Выполнять итерации в хэше можно при помощи методов **each**, **each_key**, **each_value** или **each_pair**.

Метод **each** вызывает блок для каждого ключа и значения, он может принимать один или два параметра:

```ruby
zip.each{ |k, v| puts "#{k}/#{v}" }

# => 83110/"Turnerville"

# => 83127/"Thayne"

# => 82336/"Tipton"

# => 83112/"Turnerville"

# => 82084/"Tie Siding"

# => 83025/"Teton Village"

# => 82442/"Ten Sleep"

# => 82443/"Thermopolis"

# => 82240/"Torrington"
```
  
Метод **each_pair** подобен each, за исключением того, что он должен принимать два параметра.

Метод **each_key** передает блоку только ключи:

```ruby
zip.each_key{|key| print key, " " }

# => 83110 83127 82336 83112 82084 83025 82442 82443 82240
```
  
Метод **each_value** передает блоку все значения:

```ruby
zip.each_value{|value| print value, " " }

# => Turnerville Thayne Tipton Turnerville Tie Siding Teton Village Ten Sleep Thermopolis Torrington
```
---

## **Изменяем хэши**

Метод **[]=** замещает или добавляет пары "ключ-значение" в существующий хэш:

```ruby
rhode_island = { 1 => "Bristol", 2 => "Kent", 3 => "Newport", 4 => "Providence", 5 => "Washington"}

rhode_island[6]= "Dunthorpe"
```

Добавилось значение "Dunthorpe" с ключом 6. Или методом []= можно пользоваться для изменения значения:

```ruby
rhode_island[2]= "Bent"
```

Значение связанное с ключом 2 изменилось на "Bent".

Аналогично, чтобы добавить пару в rhode_island, можно применить метод **store**:

```ruby
rhode_island.store(6, "Dunthorpe")
```
---

## **Объединяем хэши**

Возьмем два хэша:

```ruby
delaware = { 1 => "Kent", 2 => "New Castle", 3 => "Sussex" }

rhode_island = { 1 => "Bristol", 2 => "Kent", 3 => "Newport", 4 => "Providence", 5 => "Washington"}
```

Метод **merge** объединяет два хэша вместе, производя копию, из которой удалены двойные ключи путем перезаписи пар "ключ-значение" в принимающем хэше:

```ruby
rhode_island.merge delaware

# => { 5 => "Washington", 1 => "Kent", 2 => "New Castle", 3 => "Sussex", 4 => "Providence" }
```

Ключи и значения из delaware перехватили пары с такими же ключами в rhode_island, заставив Bristol, Kent и Newport исчезнуть.

Можно вместе с **merge** применить блок:

```ruby
rhode_island.merge (delaware) {|key, old, new| new = old + "_new" }

# => { 5 => "Washington", 1 => "Bristol_new", 2 => "Kent_new", 3 => "Newport_new", 4 => "Providence" }
```
---

## **Сортировка хэшей**

Если вы сортируете хэш методом **sort**, то получаете многомерный массив двухэлементных массивов:

```ruby
rhode_island = { 1 => "Bristol", 2 => "Kent", 3 => "Newport", 4 => "Providence", 5 => "Washington"}

p rhode_island		 		# => { 5 => "Washington", 1 => "Kent", 2 => "New Castle", 3 => "Sussex", 4 => "Providence" }

rhode_island.sort			 # => [ [1, "Bristol"], [2, "Kent"], [3, "Newport"], [4, "Newport"], [5, "Washington"] ]
```
---

## **Удаляем и очищаем хэш**

Удалить пару "ключ-значение" в хэше можно при помощи метода **delete**, он использует ключ для поиска пары:

```ruby
rhode_island.delete(5) # => "Washington"
```

При вызове **delete** можно передать блок, если ключ не найден, то выполняется блок:

```ruby
rhode_island.delete(5) { |key| puts "not found, bubba" }
```

Метод **delete_if** использует блок и удаляет из хэша пары "ключ-значение", для которых блок вычисляет значение true:

```ruby
rhode_island.delete_if { |key, value| key < 3 }

# => {5 => "Washington", 3 => "Newport", 4 => "Providence"  }
```

или удаление по значению:

```ruby
rhode_island.delete_if { |key, value| value == "Kent" }

# => { 5 => "Washington", 1 => "Bristol", 3 => "Newport", 4 => "Providence" }
```

Метод **reject!** Работает совсем как delete_if, но выполняет свои изменения по месту.

Метод **clear** удаляет все пары "ключ-значение", оставляя его пустым:

```ruby
counties = { "Dalaware" => 3, "Rhode Island" = 5 }

counries.clear

counties.empty?			 # => true
```
---

## **Преобразуем хэш в другие классы**

```ruby
fitzgerald = { 1920 => "This Side of Parafise", 1925 => "The Great Gatsby", 1934 => "Tender Is the Night" }
```

Можно преобразовать хэш в массив методом **to_a**:

```ruby
fitzgerald.to_a

# => [ [1925, "The Great Gatsby"], [1920, "This Side of Parafise"], [1934, "Tender Is the Night"] ]
```

Можно преобразовать в строку методом **to_s**:

```ruby
fitzgerald.to_s

# => "1925The Great Gatsby1920This Side of Parafise1934Tender Is the Night"
```
