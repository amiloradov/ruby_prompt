# **КЛАССЫ**

Класс определяется при помощи ключевого слова _**class**_, за которым следует _**end**_:

```ruby
class Hello
	def initialize(name)
	@name = name
	end

	def hello_world
	puts "Hello, #{@name}!"
	end
end

hi = Hello.new("World")
hi.hello_world				 # => Hello, World!
```
---
  
## **Аксессоры**

Метод _**attr_reader**_ автоматически создает одну или несколько переменных экземпляра с соответствующими методами, которые возвращают (берут) значения каждого метода.

Метод _**attr_writer**_ автоматически создает одну или несколько переменных экземпляра с соответствующими методами, которые устанавливают значения каждого метода.

Метод _**attr_accessor**_ выполняет для одного или более методов экземпляра класса ту же самую работу, что и методы attr_reader и attr_writer вместе взятые.

```ruby

class Dog
	attr_reader :bark
	attr_writer :age
	attr_accessor :name
end
```
---

## **Наследование**

В Ruby поддерживается одиночное наследование, что означает, что класс может наследовать только от одного класса — родительского класса или суперкласса. Дочерний класс получает доступ к методам родителя. Наследование совершается с помощью оператора <.

```ruby
class Name
	attr_accessor :given_name, :family_name
end

class Address < Name
	attr_accessor :street, :city, :state, :country
end
```

Если бы класс Name находился в отдельном файле (например, name.rb), то пришлось бы сначала затребовать этот файл:

```ruby
require 'name'

class Address < Name
	attr_accessor :street, :city, :state, :country
end
```
  ---

## **Методы public, privte и protected**

Видимость или тип доступа методов и констант может быть установлен при помощи методов public, privte и protected:

* Член класса, отмеченный как _**public**_, доступен всем и отовсюду; это значение устанавливается по умолчанию.

* _**private**_ означает, что получателем метода всегда является текущий объект или self, так что его областью видимости всегда является текущий объект (часто это вспомогательные методы, т. е. методы, которые вызываются другими методами для выполнения некоторой работы).

* Метод _**protected**_, может использоваться только экземплярами класса, в котором он был определен, или порожденными классами.

```ruby
class Names
	def initialize(given, family, nick, pet)
		@given = given
		@family = family
		@nick = nick
		@pet = pet
	end
	
# эти методы по умолчанию имеют доступ _**public**_
	def given
		@given
	end

	def family
		@family
	end

# все нижеследующие методы имеют тип _**private**_ до тех пор, пока он не будет сменен
private

	def nick
		@nick
	end

# все нижеследующие методы имеют тип _**protected**_ до тех пор, пока он не будет сменен
protected

	def pet
		@pet
	end
end


name = Names.new("Klyde", "Kimball", "Abner", "Teddy Bear")

name.given 				# => "Klyde"
name.family 			# => "Kimball"

name.nick 				# => вызовет ошибку
name.pet 				# => вызовет ошибку
```

Также метод можно вызывать после определения:

```ruby
def pet
	@pet
end

protected :pet
```
---

## **Модули**

Модуль подобен классу, но для него нельзя создать экземпляр. Модуль включается в класс и этот класс собственность включенного модуля. Имя модуля должно начинать с большой буквы. Модуль может наследовать от другого модуля, но не от класса.

```ruby
module Dice

	def roll
		r_1 = rand(6) + 1
		r_2 = rand(6) + 1
		total = r_1 + r_2
		puts "You rolled #{r_1} and #{r_2}. Total: #{total}"
	end
end

class Game
include Dice
end

g = Game.new
g.roll
```

Если модуль находиться в отдельном файле, то нужно затребовать файл с помощью _**require**_:

#Файл *dice.rb*:

```ruby
module Dice
	def roll
		r_1 = rand(6) + 1
		r_2 = rand(6) + 1
		total = r_1 + r_2
		puts "You rolled #{r_1} and #{r_2}. Total: #{total}"
	end
end
```
---

```ruby
require 'dice'

class Game
include Dice
end

g = Game.new
g.roll
```
  
Когда вы указываете в качестве префикса имя модуля, вы можете вызвать метод откуда угодно, как в случае с модулем Math.

```ruby
module Binary
	def Binary.to_bin(num)
		bin = sprinf("%08b", num)
	end
end

Binary.to_bin(123)			 # => "01111011"
```
---
