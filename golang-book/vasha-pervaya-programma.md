# Ваша первая программа

Традиционно первая программа, с которой начинается изучение любого языка программирования, называется «Hello World» — эта программа просто выводит в консоль строку `Hello World`. Давайте напишем её с помощью Vala.

Сначала создадим новую директорию, в которой будем хранить нашу программу. Установщик, о котором говорилось в первой главе, создал в вашей домашней директории каталог Vala. Теперь создайте директорию под названием `~/Vala/src/vala-book/chapter2` \(где `~` означает вашу домашнюю директорию\). Вы можете сделать это из терминала с помощью следующих команд:

```text
mkdir Go/src/golang-book
mkdir Go/src/golang-book/chapter2
```

Используя текстовый редактор, введите следующее:

{% tabs %}
{% tab title="Vala" %}
```csharp
// this is a comment
void main() {
    print("Hello World\n");
}
```
{% endtab %}

{% tab title="Golang" %}
```go
package main

import "fmt"

// this is a comment

func main() {
    fmt.Println("Hello World")
}
```
{% endtab %}
{% endtabs %}

Убедитесь, что содержимое файла идентично показанному здесь примеру, и сохраните его под именем `main.vala` в созданной ранее директории. Затем откройте новое окно терминала и введите:

{% tabs %}
{% tab title="Vala" %}
```bash
cd Vala/src/golang-book/chapter2
vala main.vala
```
{% endtab %}

{% tab title="Golang" %}
```bash
cd Go/src/golang-book/chapter2
go run main.go
```
{% endtab %}
{% endtabs %}

В окне терминала вы должны увидеть сообщение `Hello World`. Команда  `vala` берет указанные файлы \(разделенные пробелами\), компилирует их в исполняемые файлы, сохраняет во временной директории и запускает. Если вы не увидели `Hello World`, то, вероятно, где-то была допущена ошибка, и компилятор подскажет вам, где конкретно. Как и большинство компиляторов, компилятор Go крайне педантичен и не прощает ошибок.

### Как читать программу на Vala

Пакеты в Vala указываются в виде флагов во время компиляции. Например 

`vala main.vala --pkg gee-0.8` 

{% hint style="info" %}
В настоящих проектах вы скорее всего будете использовать [Meson](https://mesonbuild.com/Vala.html)
{% endhint %}

Для разграничения конфликтов имен можно использовать namespace.

{% hint style="info" %}
В namespace можно помещать любой код, кроме других namespace. 
{% endhint %}

Для этого в Vala есть 2 способа

Традиционный:

```csharp
using Gee;

namespace Foo {
    class Bar {}
    enum BarType {ONE, TWO}
    struct BarKeeper { ArrayList<string> name; }
}
```

И альтернативный:

```csharp
using Gee;

class Foo.Bar {}
enum Foo.BarType {ONE, TWO}
struct Foo.BarKeeper { ArrayList<string> name; }
```

Вторая версия намного чище \(не добавляет дополнительного уровня отступов\)

using означает что в данном файле используется namespace. Например в примере выше ArrayList находится в namespace Gee. Но благодаря using Gee можно писать просто ArrayList вместо Gee.ArrayList



```csharp
// this is a comment
void main() {
    print("Hello World\n");
}
```

Строка, начинающаяся с `//`, является комментарием. Комментарии игнорируются компилятором Go и служат пояснениями исключительно для вас \(или для тех, кто будет потом читать ваш код\). Go поддерживает два вида комментариев: `//` превращает в комментарий весь текст до конца строки и `/* */`, где комментарием является всё, что содержится между символами `*` \(включая переносы строк\).

Далее можно увидеть объявление функции:

{% tabs %}
{% tab title="First Tab" %}
```csharp
void main() {
    print("Hello World\n");
}
```
{% endtab %}

{% tab title="Second Tab" %}
```go
func main() {
    fmt.Println("Hello World")
}
```
{% endtab %}
{% endtabs %}

Функции являются кирпичиками программы на Vala. Они имеют входы, выходы и ряд действий, называемых операторами, расположенных в определенном порядке. Любая функция начинается с типа возвращаемого значения за которым следуют: имя функции \(в нашем случае `main`\), список из нуля и более параметров в круглых скобках и само «тело», заключенное в фигурные скобки. Наша функция не имеет входных параметров, ничего не возвращает\(`void`\) и содержит всего один оператор. Имя `main` является особенным, эта функция будет вызываться сама при запуске программы. \(Вы можете изменить это поведение с помощью флага `--main=SYMBOL`\)

Заключительной частью нашей программы является эта строка:

{% tabs %}
{% tab title="Vala" %}
```csharp
print("Hello World\n");
```
{% endtab %}

{% tab title="Golang" %}
```go
fmt.Println("Hello World")
```
{% endtab %}
{% endtabs %}

Этот оператор содержит  две части: функция под названием `print`, затем создание новой строки, содержащей `Hello World`, и вызов функции с этой строкой в качестве первого и единственного аргумента.

На данный момент вы уже можете быть немного перегружены количеством новых терминов. Иногда полезно не спеша прочесть вашу программу вслух. Программу, которую мы только что написали, можно прочитать следующим образом:

Создать новую исполняемую программу, которая содержит функцию `main`. Эта функция не имеет аргументов, ничего не возвращает и делает следующее: использует функцию `Println` из библиотеки `fmt` и вызывает её, передавая один аргумент — строку `Hello World`.

Функция `Println` выполняет основную работу в этой программе. Вы можете узнать о ней больше, набрав её имя в поиске Valadoc: [https://valadoc.org/glib-2.0/GLib.print.html](https://valadoc.org/glib-2.0/GLib.print.html)

Vala — хорошо документированный язык, но эта документация может быть трудна для понимания, если вы до этого не были знакомы с другими языками программирования. Тем не менее, [ValaDoc](https://valadoc.org/glib-2.0/index.htm)  и [GNOME  Vala Wiki](https://wiki.gnome.org/Projects/Vala/Documentation) являются очень полезеными ресурсами для начала поиска ответов на возникающие вопросы. 

В следующей главе вы поймете, каким образом Vala хранит и представляет вещи вроде `Hello World` с помощью типов.



### Задачи

* Что такое разделитель?
* Что такое комментарий? Назовите два способа записи комментариев.
* * Мы использовали функцию `print`. Если бы мы хотели использовать функцию **`get_host_name`** из namespace `Environment`, что бы для этого потребовалось сделать?
* Измените написанную программу так, чтобы вместо `Hello World` она выводила `Hello, my name is` вместе с вашем именем.
