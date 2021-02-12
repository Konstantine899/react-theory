# setState() - удаление элемента 

Давайте продолжим писать наш код который должен удалять элементы из нашего списка.

И так у нас есть компонент **App** у которого есть данные, массив наших элементов которые мы используем для списка.

![](../img/component__status__and__event__handling/setstate__delete__element/001.jpg)


Соответственно если мы обновим этот массив. Удалим нужный элемент, а затем приложение обновится, то наш компонент пропадет.

Единственная проблема заключается в том что **App** сейчас является компонентом Функцией и у него нет **state** т.е. *состояния*.
Соответственно даже если мы удалим правильный элемент из этого массива

![](../img/component__status__and__event__handling/setstate__delete__element/002.jpg)

react не узнает что остаток приложения нужно обновить.

Для того что бы react обновил приложение, компонент **App**

![](../img/component__status__and__event__handling/setstate__delete__element/003.jpg)

нужно сделать компонентом **class**. А **todoDate** 

![](../img/component__status__and__event__handling/setstate__delete__element/004.jpg)

cделать частью **state** частью состояния приложения. 
Тогда мы будем вызывать функцию **setState** а это всвою очередь даст знать react о том что приложение нужно обновить.

И так приступим. Для начала сделаем наш простой рефакторинг и сделаем из компонента App компонент класс.

Импортируем компонент для того что бы его extend-дить (расспостранять).

![](../img/component__status__and__event__handling/setstate__delete__element/005.jpg)

И **const App** заменяем на **export default class App**

![](../img/component__status__and__event__handling/setstate__delete__element/006.jpg)

![](../img/component__status__and__event__handling/setstate__delete__element/007.jpg)

Extends Component- в переводе рассширяет компонент.

Cледующим шагом **todoDate**, наш массив, становится частью state, состояния.

![](../img/component__status__and__event__handling/setstate__delete__element/008.jpg)

И это свойства наш массив.

![](../img/component__status__and__event__handling/setstate__delete__element/009.jpg)

![](../img/component__status__and__event__handling/setstate__delete__element/010.jpg)

помещаем этот JSX элемент в функцию render.

 ![](../img/component__status__and__event__handling/setstate__delete__element/011.jpg)

 Меняем на **this.state.todoDate**
 Ну и конечно удаляем последнюю строку с экспортом.

  ![](../img/component__status__and__event__handling/setstate__delete__element/012.jpg)

  Ок! Теперь у нас появился компонент class. 
  И теперь мы можем написать функцию которая будет удалять наш элемент.

![](../img/component__status__and__event__handling/setstate__delete__element/013.jpg)

![](../img/component__status__and__event__handling/setstate__delete__element/014.jpg)

Создаем функцию **deleteItem** и мы ее объявим в теле класса функции стрелки. Мы будем передавать эту функцию как event lisener, слушатель событий, нам надо убедиться что значение this этой функции останется корректным. 
    Давайте напишем что мы собираемся удалять элемент с каким-то id.

![](../img/component__status__and__event__handling/setstate__delete__element/015.jpg)

![](../img/component__status__and__event__handling/setstate__delete__element/016.jpg)

Если мы сделали все правильно мы должны получать числа в консоли которые показывают на id  элемента который нам нужно удалить

![](../img/component__status__and__event__handling/setstate__delete__element/017.jpg)

Теперь можно перейти к самому удалению.
И сдесь есть вопрос. В функции deletItem удаляем вызов консоли. А вместо этого естественно вызываем **this.setState()**. Но вот только в какой форме мы ее будем вызывать?

![](../img/component__status__and__event__handling/setstate__delete__element/018.jpg)

Надо подумать передать туда объект с новым состоянием state, илиже передать функцию которая будет принимать state и возвращать новое состояние?

И конечно же мы должны передать функцию потому что нам нужно установить новый state, новое состояние. А новый state это старый массив без одного элемента. 
Но для того что бы сделать старый массив без одного элемента нам нужно знать какой именно был старый массив. И поэтому наш новый state зависит от старого state. Поэтому нам нужна функция. Мы не можем просто так взять и передать туда объект.

![](../img/component__status__and__event__handling/setstate__delete__element/019.jpg)

todoDate будем использовать в теле этой функции.

![](../img/component__status__and__event__handling/setstate__delete__element/020.jpg)

Для того что бы вычислить новое состояние, state, нам необходимо удалить из массива элемент. Сделать это можно несколькими способами. Давайте для начала получим индекс того элемента который мы собрались удалять.
**сonst id = todoDate.findIndex((el) => el.id === id);** Мы говорим TodoData найди там индекс. В параметрах пишем елемент у которого id эквивалентен тому id  который мы получили.

![](../img/component__status__and__event__handling/setstate__delete__element/021.jpg)

Для проверки выведем в консоль.

![](../img/component__status__and__event__handling/setstate__delete__element/022.jpg)

Есть мы получаем правильный индекс. Соответственно мы готовы удалять элемент. И удаляем элемент методом **splice**. Splise вытащит элемент из массива, сделает массив меньше и вернет назад тот элемент который мы удалили.

![](../img/component__status__and__event__handling/setstate__delete__element/023.jpg)

**todoData.splice(idx,1);** Вторым параметром указываем удаляемый индекс.

И далее с помощью return возвращаем новое состояние **todoData : todoData**

![](../img/component__status__and__event__handling/setstate__delete__element/024.jpg)

Tcnm еще одна проблема!!! Мы нарушаем одно из самых главных правил react. Мы редактируем и изменяем предыдущий state состояние. 
Когда мы вызываем функцию setState

![](../img/component__status__and__event__handling/setstate__delete__element/025.jpg)

к нам приходит объект в котором находится старый state. Мы достаем из этого объекта массив **todoData** и прямо внутри этого массива мы удаляем элемент.

![](../img/component__status__and__event__handling/setstate__delete__element/026.jpg)


Соответственно наш старый массив в предыдущем state состоянии он изменился и мы нарушили то самое правило **не изменять state на прямую**.
Может быто из этого кода не сильно очевидно, нет сдесь кода который берет this.state и что-то меняет, но посути это то что мы делаем.
Мы получаем массив и затем изменяем его.

![](../img/component__status__and__event__handling/setstate__delete__element/027.jpg)

>*Нам не вкоем случае нельзя изменять те структуры данных которые мы получаем внутрь setState. Это очень плохая практика которая приводит к ошибкам которые сложно отлавливать.*


Вместо этого нам нужно вернуть новый массив который содержит все элементы старого массива кроме того элемента который мы хотим удалить.

Как сделать новый массив не трогая при этом старый массив?

![](../img/component__status__and__event__handling/setstate__delete__element/028.jpg)

Как получить два элемента перед *c**?
Создаем **const before =**, переводится как до, и для того что бы получить эти элементы мы будем использовать метод **slice**. Метод **slice** не изменяет существующий массив поэтому нам можно его использовать.

![](../img/component__status__and__event__handling/setstate__delete__element/029.jpg)

slise в параметрах принимает два аргумента. Начало и конец сегмента который мы будем копировать. Начало сегмента у нас **0**, а конец сегмента это id который мы собираемся удалить

![](../img/component__status__and__event__handling/setstate__delete__element/030.jpg)

Соответственно **const after =**,переводится как после, будет работать точно так же для второй половины которую мы реконструируем т.е. для тех элементов id которых будет после удаленного элемента.

![](../img/component__status__and__event__handling/setstate__delete__element/031.jpg)

![](../img/component__status__and__event__handling/setstate__delete__element/032.jpg)

В параметрах пишем **(idx + 1)** поскольку сам индекс пропадает до конца. Если мы не передаем второй аргумент то это как раз будет означать от этого индекса и до самого конца массива.

![](../img/component__status__and__event__handling/setstate__delete__element/033.jpg)

И теперь новый массив будет выглядеть так. Используем spread спред оператор для массивов.
И далее передаем этот массив в todoData в качестве нового состояния 

![](../img/component__status__and__event__handling/setstate__delete__element/034.jpg)

Вот таким вот способом удаляем элемент из массива так что бы не изменять массив. Метод slice  не изменяет массив, он просто копирует элементы и затем конструирует новый массив из всех жлементов до нужного и все элементы после него.

Код работает все удаляется. 

Давайте немного отрефакторим этот код. Насамом деле константы before and arter  нужны очень наглядно что бы показать как работает этот метод.

![](../img/component__status__and__event__handling/setstate__delete__element/035.jpg)

Уже не нужные константы before и after удаляем.

![](../img/component__status__and__event__handling/setstate__delete__element/036.jpg)

Мы только что освоили один из самых сложных элементов react а именно не изменность state состояния.

![](../img/component__status__and__event__handling/setstate__delete__element/037.jpg)





