## Константы, литералы, магические числа и валидации

Ты уже написал несколько программ на Go, в которых используются условия и логические переменные. Теперь нужно сделать их более понятными и надёжными.

### 🧠 Что нужно знать:

#### Литерал 
Литерал — это просто напрямую написанное значение в коде: `18`, `"yes"`, `"friday"` — всё это литералы.

#### Магическое значение
Магическое значение — это литерал, смысл которого **не очевиден**.


```go
if score >= 60 {
	fmt.Println("Вы сдали экзамен")
} else {
	fmt.Println("Вы не сдали")
}
```

На первый взгляд — вроде всё понятно. Но **почему 60?**
— Это проходной балл?
— А если завтра изменится порог?

Если в коде есть просто **60**, **без пояснений** — это **магическое значение**. Оно может встретиться в десяти местах, и если нужно его изменить, придётся искать везде. А главное — **новому читателю кода непонятно, что это такое.**

Тот же код с константами (хорошо):

```go
const passingScore = 60

if score >= passingScore {
	fmt.Println("Вы сдали экзамен")
} else {
	fmt.Println("Вы не сдали")
}
```

Теперь:

* Понятно, что `60` — это **порог сдачи**;
* Если порог изменится, достаточно поменять **одну строчку**;
* Код **читабельнее и надёжнее**.

#### Валидация
Валидация — это проверка, что пользователь ввёл **корректные данные**. Например, что возраст - это не отрицательное число.

#### return
Когда в функции `main()` встречается `return`, программа **сразу завершает работу**. Это полезно, если ввод неправильный:

```go
const minAge = 1
const maxAge = 150

if age < minAge || age > maxAge {
	fmt.Println("Некорректный возраст")
	return // завершить программу
}
```

---

### ✅ Задание:

Ниже приведён пример — **оформленная и улучшенная** версия задачи *«Разрешение на ночную вечеринку»*. Она использует **константы**, выполняет **валидацию ввода** и корректно завершает программу при ошибке. Твоя задача — оформить **остальные задачи из урока 5 таким же образом**.

Обрати внимание:

* Все важные значения должны быть записаны как константы с понятными именами.
* Валидация должна проверять правильность ввода и останавливать программу при ошибке.
* Ошибки должны сопровождаться понятным сообщением.
* Если всё введено верно — программа продолжает работать как обычно.

---

💡 Это задание поможет тебе научиться писать **чистый, понятный и устойчивый код**. Даже простая программа должна быть надёжной 💪

Пример кода:

```go
/* Задача 4. Разрешение на ночную вечеринку

Пользователь вводит:
- Возраст
- Разрешение от родителей (yes / no)
- День недели (friday, saturday, sunday, monday, и т.д.)

Создайте логические переменные:
isLegal               - true, если возраст ≥ 18
hasParentalPermission - true, если введено "yes"
isWeekend             - true, если день — friday или saturday

Создайте итоговую переменную для if:
canGoToParty - true, если человек ≥ 18 ИЛИ есть разрешение и это выходной

Вывод: "Можете проходить" или "Мы не можем вас пропустить"
*/ 

package main

import "fmt"


func main() {
	fmt.Println("Ваш возраст:")

	var age int
	fmt.Scanln(&age)

	const minAge = 1
	const maxAge = 150

	if age < minAge || age > maxAge {
		fmt.Println("Некорретный возраст")
		return
	}

	fmt.Println("Есть ли разрешение от родителей? (yes/no)")

	var parentalPermission string
	fmt.Scanln(&parentalPermission)

	const yes = "yes"
	const no = "no"

	if parentalPermission != yes && parentalPermission != no {
		fmt.Println("Некорректный ответ на вопрос")
		return
	}

	fmt.Println("Введите день недели:")
	
	var dayOfWeek string
	fmt.Scanln(&dayOfWeek)
		
	const monday = "monday"
	const tuesday = "tuesday"
	const wednesday = "wednesday"
	const thurday = "thurday"
	const friday = "friday"
	const saturday = "saturday"
	const sunday = "sunday"

	if dayOfWeek != monday &&
	   dayOfWeek != tuesday &&
	   dayOfWeek != wednesday &&
	   dayOfWeek != thurday &&
	   dayOfWeek != friday &&
	   dayOfWeek != saturday &&
	   dayOfWeek != sunday {
		
		fmt.Println("Некорректный день недели")
	}	

	const legalAge = 18

	isLegal := age >= legalAge

	hasParentalPermission := parentalPermission == yes

	isWeekend := dayOfWeek == friday || dayOfWeek == saturday

	canGoToParty := isLegal || (hasParentalPermission && isWeekend)

	if canGoToParty {
		fmt.Println("Можете проходить")
	} else {
		fmt.Println("Мы не можем вас пропустить")
	}
}
```
