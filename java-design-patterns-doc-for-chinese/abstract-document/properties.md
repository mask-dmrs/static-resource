# 属性的行为(校对中)
---
*Martin Fowler*   <P>
fowler@acm.org

---
- [<span id="1">你创建的每个对象几乎都需要属性：关于对象的一些声明。一个人可能有一个身高属性，一个公司可能有一个CEO，一个航班可能有一个航班号。有很多方法来创建属性。在这篇文章中，我将探讨其中一些你经常需要用到的方法。我经常看到涉及到这个话题的图案，但他们通常只涉及一部分。在这里，我想更广泛地讨论这个问题，以便更好地讨论这些选项。</span>](#1 "Almost every object you create needs properties: some statement about the object. A person may have a height, a company may have a CEO, a flight may have a flight number. There are a number of ways to model properties. In this article I will explore some of these ways and when you may want to use them. I’ve often seen patterns touch on  this subject, but they usually only cover part of the picture. Here I want to cover the issue  more broadly to give a better discussion of the options.")

- [<span id="2">最常见和最简单的情况是使用`固定属性`，即只声明类的属性。在绝大多数情况下，你只需要使用`固定属性`。在有大量固定属性或者需要频繁修改时，使用`固定属性`容易出错。这种情况下你可能会使用`动态属性`。所有的`动态属性`都有一个参数化属性的特性：你需要一个带参的方法来查询一个属性。当参数只是一个字符串,最简单的是`灵活的动态属性`。这样定义和使用属性会比较容易，但难以控制。如果你需要使用`动态属性`，在你的参数必须是一个类的实例的情况下。使用类型`动态属性`来增强对`动态属性`的控制。</span>](#2 "The most common, and the simplest case is to use a Fixed Property , that is just declare the attribute on the class. In the vast majority of cases that is all you need to do. Fixed properties begin to fail when you have a large amount of them, or you need to change them frequently, possibly at run time. These forces lead you to the varieties of Dynamic Property . All dynamic properties have the quality of a parameterized attribute where to query a property you need to use a query method with a parameter. The simplest of these is the Flexible Dynamic Property where the parameter is just a string. This makes it easy to define and use properties, but is difficult to control. If you need that control you can use a Defined  Dynamic  Property  where  your parameters must be instances of some class. A further step of control allows you to strongly type your dynamic property with a Typed Dynamic Property .")

- [<span id="3">随着您的属性结构变得越来越复杂，您应该考虑将它们设置为“单独属性”，把一些属性综合起来创建一个对象。如果你需要多值属性，你可以考虑集合。在这篇文章中最复杂的例子是你想要规则来控制什么类型的对象具有什么样的属性 - 这需要一定的`动态属性`知识水平。</span>](#3 "As your property structures get more involved, you should consider making them Separate Properties , which makes the property an object in its own right. If you need multi-valued properties you can consider a Typed Relationship . The most complex example in this theme is where you want rules to control what kinds of objects have what kinds of properties – this needs a Dynamic Property Knowledge Level .")

- [<span id="4">另一种属性完全是`外部属性`（Extrinsic Property），如果你想使用接口给一个对象创建一个属性，那么这就是你需要使用的一种模式。<span>](#4 "Another variety of property entirely is the Extrinsic Property , a pattern you use if you want to give an object a property, but not alter its interface to support it.")

[<span id="5">问题</span>](#5 "Problem")	|[<span id="5">答案</span>](#5 "Solution")	|[<span id="5">名称</span>](#5 "name")	|[<span id="5">页码</span>](#5 "page")
--- | --- | --- | ---
 &nbsp;  |[<span id="6">在编程语言里，当使用一个特定的属性，它需要查询或者更新。<span>](#6 "Give it a specific attribute for that fact. This will translate to a query method and probably an update method in a programming language.")|[`固定属性`](#固定属性 "Fixed Property")|4
 &nbsp;  |[<span id="7">提供可参数化的属性，可以根据参数表示不同的属性</span>](#7 "Provide a parameterizable attribute which can represent different properties depending on the parameter")|[`动态属性`](#动态属性 "Dynamic Property")|4
 &nbsp;  |[<span id="8">提供一个用字符串参数化的属性。声明一个属性只是使用字符串.](#8 "Provide an attribute parameterized with a string. To declare a property just use the string.")|[`灵活的动态属性`](#灵活的动态属性 "Flexible Dynamic Property")|5
 &nbsp;  |[<span id="9">提供用某种类型的实例参数化的属性。要声明属性，请创建该类型的新实例</span>](#9 "Provide an attribute parameterized with an instance of some type. To declare a property create a new instance of that type")|[`定义动态属性`](#定义动态属性 "Defined Dynamic Property")|7
 &nbsp;  |[<span id="10">提供使用某种类型的实例进行参数化的属性。要声明属性，请创建该类型的新实例并指定该属性的值类型.</span>](#10 "Provide an attribute parameterized with a instance of some type. To declare a property create a new instance of the type and specify the value type of the property.")|[`类型动态属性`](#类型动态属性 "Typed Dynamic Property")|9
[<span id="11">你如何表示一个对象的属性，并允许对象的属性也具有属性</span>](#11 "How do you represent a fact about an object, and allow facts to be recorded about that fact")|[<span id="11">为每个属性创建一个单独的对象。 关于那个属性的详细可以作为这个对象的的属性.<span>](#11 "Create a separate object for each property. Facts about that property can then be made properties of that object.")|[`分离属性`](#分离属性 "Separate Properties")	|10
[<span id="12">你如何表示两个对象之间的关系（如何表示多个值动态属性？）</span>](#12 "How do you represent a relationship between two objects?(How do you represent multi-valued dynamic properties?)")|[<span id="12">为两个对象之间的每个链接创建一个关系对象。 给关系对象一个类型对象来表示关系的含义。 （类型对象是多值属性的名称。）<span>](#12 "Create a relationship object for each link between the two objects. Give the relationship object a type object to indicate the meaning of the relationship. (The type object is the name of the multi-valued property.)")|[`类型关系`](#类型关系 "Typed Relationship")| 14
[<span id="13">当你使用动态属性时，你如何强制某些类型的对象具有某些属性？</span>](#13 "How do you enforce that certain kinds of objects have certain properties when you use dynamic properties?") |[<span id="13">创建知识级别以包含哪些类型的对象使用哪些类型的属性的规则](#13 "Create a knowledge level to contain the rules of what types of objects use which types of properties") |[`动态属性知识水平`](#动态属性知识水平 "Dynamic Property Knowledge Level")| 16
[<span id="14">你如何给一个对象新增一个属性而不改变它的接口？</span>](#14 "How do you give an object a property without changing its interface?")|[使用另一个对象负责属性](#14  "Make another object responsible for knowing about the property")| [`外在性质`](#外在性质 "Extrinsic Property")| 18

---
## 什么是属性

- [<span id="15">这不是一个愚蠢的问题。当人们使用“属性”这个词时，他们可能有很多不同的含义。对某些属性来说，是一个类的实例变量或数据成员。对于其他人来说，它们就像`UML`图中的一个盒子一样。所以在我开始这篇文章之前，我必须定义这个词的用法。</span>](#15 "This is not a silly question. When people bandy around the term ‘property’ they can mean many different things. To some a property is an instance variable or data member of a class. To others they are kind of thing that goes in a box in a UML diagram. So before I start this article I have to define my usage of the word.")

- [<span id="16">为了我的目的，一个属性是关于一个可以通过查询方法获得的对象的一些信息。它可能是一个值类型（如`Java`中的`int`）或一个类的实例。您可能能够修改该属性，但不一定。您可以在创建对象时设置属性，但不一定。该属性可以作为实例变量或数据成员存储，但不一定是。班级可能会从另一个班级获得值，或者经过一些进一步的计算。因此，我采用属性的接口视图而不是实现视图。这是我在设计中经常使用的习惯：对于我来说，面向对象的本质是将接口与实现分开，并使接口更加重要。](#16 "For my purposes a property is some information about an object that you can obtain by a query method. It may be a value type (such as int in Java) or an instance of a class. You may be able to update the property, but not necessarily. You may set the property when you create the object, but again not necessarily. The property may be stored as an instance variable or data member, but it does not have to be. The class may get the value from another class, or go through some further calculation. I am, therefore, taking an interface view of properties rather than an implementation view. This is a regular habit of mine in design: for me the essence of object-orientation is that you separate interface from implementation, and make interface more important.")
---

## <span id = "固定属性">固定属性</span>
- [<span id="17">`固定属性`是我们使用的最常见的属性。 固定属性在类型的接口中声明。 它给出了属性的名称和返回类型。 图1显示了使用`UML`建模的属性，示例1显示了这些属性的查询方法如何在`Java`中使用。 我已经选择了这个例子来说明这个讨论同样适用于`UML`属性和`UML`关联。 它也适用于计算值（年龄）以及那些合理存储的数据（出生日期）。](#17 "Fixed properties are by far the most common kind of properties that we use. A Fixed Property is declared in the interface of the type. It gives the name and the return type for the property. Figure 1 shows properties modeled in UML, Listing 1 shows how the query methods for these properties would show up in Java. I’ve picked the example to show that this discussion applies equally well to UML attributes as well as UML associations. It also applies to calculated values (age) as well as those that are reasonably stored data (date of birth).")

![image](https://static.zuul.top/java-design-patterns-doc-for-cn/abstract-document/3_1.png)
#### 图1.使用`固定属性`建模的人员
```java
class Person {
    public Date getDateOfBirth();
    public int getAge();
    public Quantity getHeight();
    public Company getEmployer();
    public void setDateOfBirth (Date newDateOfBirth);
    public void setEmployer (Company newEmployer);
```
#### 列举,图1的`java`操作

- [<span id="18">查询操作通常遵循一些命名约定。在`程序语言`中，您总是在属性名称（`dateOfBirth`）之后命名查询。 `C++`从来没有一个固定的约定，有些人只是在属性后面命名，而另一些人则使用`get`约定（`getDateOfBirth`）。 `Java`从没有特别的约定开始，但现在大多数人都采用`get`约定。就我个人而言，当您阅读代码时，我发现`get`令人恼火，所以我宁愿忽略它，但`Java`风格是使用`get`，所以现在就使用它。无论您使用的是存储值还是派生值，都应确保遵循相同的约定。使用`Person`的客户端不应该知道或关心年龄是否存储或派生。](#18 "Query operations usually follow some naming convention. In smalltalk you always name the query after the name of the property (dateOfBirth). C++ never had a fixed convention, some people just named it after the property, others used the 'get' convention (getDateOfBirth). Java started with no particular convention but now most people adopt the get convention. Personally I find the ‘get’ irritating when you read code so I would prefer to leave it out, but the Java style is to use the get, so I use it now. You should ensure that you follow the same convention whether you are using stored or derived values. Clients of the person class should not know or care whether age is stored or derived.")

- [<span id="19">`修饰符`操作的存在取决于您是否希望直接修改值。如果你这样做，那么你会根据一些命名方案，例如`setDateOfBirth`（`Date`）提供一个修饰符操作。对于`返回值`存在不同的约定。你可以返回属性的新值（`Date`），被修改的对象（`Person`），或者什么都没有（`void`）。我更愿意在修饰符上返回`void`，以帮助明确修饰符和查询之间的区别。](#19 "The presence of modifier operations depends on whether you want the values to be directly modified. If you do then you will provide a modifier operation according to some naming scheme, eg setDateOfBirth(Date). Different conventions exist as to the return value. You can return the new value of the property (Date), the object being modified (Person), or nothing (void). I prefer to return void on modifiers, to help make clear the difference between a modifier and a query.")

---
  <h3 align = "center">固定属性</h3>
  - [<span id="20">你如何代表一个对象的事实？</span>](#20 "How do you represent a fact about an object?")
  -  [<span id="20">给它一个这个事实的特定属性。这将转化为查询方法，并可能是一种编程语言的更新方法。</span>](#20 "Give it a specific attribute for that fact. This will translate to a query method and probably an update method in a programming language.")</br>
    - [<span id="20">接口很清晰明确</span>](#20 "Clear and explicit interface")</br>
    - [<span id="20"><font color="red">只能在设计时添加属性</font></span>](#20 "Can only add properties at design time")</br>
---
  
- [<span id="21">您可能希望为属性的`构造函数`提供参数。通常，您要在`构造函数`中设置足够的属性，以便构建格式良好的类。</span>](#21 "You may wish to provide arguments to the constructor for properties. Typically you want to set enough properties in the constructor so that you construct a well-formed class.")

- [<span id="22">不想直接修改的属性不应该有`修饰符`操作。如果您只希望从出生之日起计算，那么年龄属性可能就是这种情况。对于一个不可改变的`属性`也是如此：一个在类的生命周期中不会改变的`属性`。当你想使`属性`不可改变时，请记住考虑到人为错误。虽然出生日期对于现实世界中的人类来说是不可改变的`属性`，但是您可能会在输入到计算机系统时出现错误，从而使其变得可变。软件常常模拟我们所知道的世界，而不是世界本身。</span>](#22 "Properties that you don’t want to be modified directly should not have a modifier operation.This might be the case for the age property, if you only want that determined by calculation from the date of birth. It also would be the case for an immutable property: one that does not change for the lifetime of the class. When you think of making a property immutable, remember to take human error into account. While the date of birth is an immutable property for humans in the real world, you might make a mistake typing into a computer system, and thus make it mutable. Software often models what we know of the world, rather than the world itself.")

- [<span id="23">`固定属性`是迄今为止您将遇到的最常见的`属性`形式。他们这样做是有原因的：他们使用简单方便。您应该使用固定属性作为表示属性的第一个也是最常见的选择。在本文中，我将给出许多固定属性的替代方案。在某些情况下，这些替代品更好，但大多数情况下不是。请记住，当我们经历的选择。我99％的时间使用固定的属性。其他品种更为复杂，这就是为什么我把这篇论文的大部分花费在他们身上 - 也是为什么我不愿意使用它们！</span>](#23 "Fixed properties are by far the most common form of properties that you will come across.They are that way for good reasons: they are simple and convenient to use. You should use fixed properties as your first and most common choice for representing properties. In this paper I am going to give a lot of alternatives to fixed properties. For certain situations these alternatives are better, but most of the time they are not. Remember that as we go through the alternatives. I use fixed properties 99% of the time. Other varieties are more complex, which is why I'm spending most of this paper on them — and also why I prefer not to use them!")

## <span id = "动态属性">动态属性</span>
- [<span id="24">`固定属性`的关键在于您在设计时修复了这些属性，并且所有实例在运行时都必须遵循该决定。 对于一些问题，这是一个尴尬的限制。 想象一下，我们正在建立一个复杂的联络系统。 有一些东西是固定的：家庭住址，家庭和工作电话，电子邮件。 但他们是各种各样的小变化。 对于需要记录父母地址的人，另一个人有白天工作和晚上工作号码。 事先很难预测所有这些事情，每次更改系统时都必须经过编译，测试和分发。 要处理这个问题，你需要使用动态属性。</span>](#24 "The key thing about fixed properties is that you fix them at design time, and all instances at run time must follow that decision. For some problems this is an awkward restriction. Imagine we are building a sophisticated contact system. There are some things that are fixed: home address, home and work phone, email. But they’re all sorts of little variations. For someone you need to record their parent’s address, another has a day work and evening work numbers.It’s hard to predict all these things in advance, and each time you change the system you have to go through compiling, testing, and distribution. To deal with this you need to use dynamic properties.")

---
  <h3 align = "center">动态属性</h3>
  - [<span id="25">你如何代表一个对象的事实？</span>](#25 "How do you represent a fact about an object?")</br>
  - [<span id="25">提供可参数化的属性，可以根据参数表示不同的属性</span>](#25 "Provide a parameterizable attribute which can represent different properties depending on the parameter") </br>
   - [<span id="25"> 可以在运行时添加属性</span>](#25 "Can add properties at run time")
   - [<span id="25"><font color="red">接口不清晰</font></span>](#25 "Unclear interface")
---
  
- [<span id="26">`动态属性`有多种变化，每种变化都会在`灵活性`和`安全性`之间做出不同的选择。 最简单的方法是`灵活动态属性`。 这种模式的本质是为键值为简单值的人（通常是字符串）添加一个合格的关联（参见图2和示例2）。 如果您想为某人Kent添加休假地址，则只需使用清单3中的代码即可。您不需要重新编译人员类。 你甚至可以建立一个图形用户界面（`GUI`）或者文件读取器来添加属性，而不用重新编译客户端。</span>](#26 "There are several variations on dynamic properties, each of which make different trade-offs between flexibility and safety. The simplest approach is Flexible Dynamic Properties. The essence of this pattern is that you add a qualified association to the person whose key is a simple value, usually a string (see Figure 2 and Listing 2). If you want to add a vacation address to a person Kent, you just use the code in Listing 3. You don’t need to recompile the person class. You could even build a GUI or a file reader that would add properties without recompiling the client either.")

![image](https://static.zuul.top/java-design-patterns-doc-for-cn/abstract-document/5_1.png)
#### 图2.使用动态属性建模的人员
```java
class Person {
    public Object getValueOf(String key);
    public void setValueOf(String key, Object value);
```
#### 列举2,图2的`java`方法
```java
kent.setValueOf(“VacationAddress”, anAddress);
Address kentVactation = (Address) kent.getValueOf(“VacationAddress”)
```
#### 列举3,使用动态属性
- [<span id="27">这样说，你可能想知道为什么有人会使用固定的属性，因为动态的像这样的属性给了你更多的灵活性。当然有一个成本，它在于软件各部分之间依赖关系的清晰度降低。这一切都非常好给一个人增加一个度假地址属性，但是你怎么知道把它重新取回呢？有了固定的属性，你可以看看人的界面，看看属性。该编译器可以检查不要求对象做不理解的事情。 用一个动态属性，你不能做任何设计时检查。此外的界面人很难看。不只是你看`Person`的声明接口 -你也必须找到不会出现在类接口中的动态属性。你必须找到那些设置属性的代码部分（通常不会在`Person`类中）提现出来。</span>](# "Said like that, you might wonder why anyone would ever use fixed properties, since dynamic properties such as this give you so much more flexibility. Of course there is a cost, and it lies in the reduction of the clarity of the dependencies between parts of the software. It is all very well adding a vacation address property to a person, but how do you know to get it back again? With fixed properties you can just look at the interface of person and see the properties. The compiler can check that don’t ask an object to do something it doesn’t understand. With a dynamic property you cannot do any design-time checking. Furthermore the interface of person is harder to see. Not just do you look at Person’s declared interface – you also have to find the dynamic properties, which will not be present in the class interface. You have to find that part of the code that sets the property (which usually will not be in the Person class at all) and dig it out.")

---
 <h3 align = "center">灵活动态属性</h3>
  - [<span id="28">你如何代表一个对象的事实？</span>](#28 "How do you represent a fact about an object?")</br>
  - [<span id="28">提供一个用字符串参数化的属性。只声明一个属性使用字符串。</span>](#28 "Provide an attribute parameterized with a string. To declare a property just use the string.") </br> 
---

- [<span id="30">不仅是属性很难找到，它的依赖也是一个噩梦。随着固定属性的客户端代码有一个依赖于人类 - 一个依赖是难以跟踪。如果你改变属性的名字，编译器会让你知道，并告诉你需要改变什么代码才能解决问题。但灵活的动态属性创建一个依赖于任意一段代码。它可能是属于一个类的代码甚至不能被客户端看到。如果有人更改密钥字符串会发生什么？如果有人改变他们把键入字符串的对象的类型会发生？不仅仅是编译器没法帮助你，你甚至不知道从哪里开始查找变化。</span>](#30 "Not just is the property hard to find, it also creates a nightmare dependency. With fixed properties the client code has a dependency to the person class – a dependency that is easy to keep track of. If you change the name of the property the compiler will let you know, and tell you what code you need to change to fix things. But the Flexible Dynamic Property creates a dependency into some arbitrary piece of code. It could be code that belongs to a class that is not even visible to the client. What happens if someone changes the key string? What happens if someone changes the type of object they put into the key string? Not just can the compiler do nothing to help you, you don’t even know where to start looking for potential changes.")

- [<span id="31">`灵活的动态属性`在最极端的情况下显示了这个问题。 该属性可能是`Person`的任何客户端在设计时创建。 如果另一个人的客户端使用同一个属性，那么你就很难找到两个类之间的依赖关系。 此外属性可以在运行时通过读取文件或通过`GUI`添加。 即使在运行时，不可能发现一个人的哪些动态属性是合法的。 当然，你可以问一个人，如果它有一个度假地址的属性 - 但如果没有一个这是否意味着这一点人没有假期地址，或者是否意味着没有这样的度假地址属性？ 而如果现在没有这样的属性，那并不意味着它几秒钟后不会有。</span>](#31 "Flexible Dynamic Properties show this problem at it’s most extreme. The property could be created at design time by any client of Person. If another client of person uses that same property you have a dependency between two classes that is very hard to find. Furthermore properties can be added at run time by reading a file or by a GUI. It is impossible to find out, even at run time, what are the legal dynamic properties for a person. True you can ask a person if it has a property for vacation address – but if there isn’t one does that mean that that person does not have a vacation address, or does it mean that there is no such property as vacation address? And if it has no such property now, that doesn’t mean it won’t have one a few seconds later.")

- [<span id="32">灵活动态特性的另一个关键缺点是很难替代它们进行操作。封装的一个关键优势是使用属性的客户端无法分辨它是作为对象数据的一部分存储的，还是通过方法来计算的。这是一个对象方法非常重要的一部分。它可以让你不只是一个普通的接口实现，而且在客户端不知情的情况下改变你期望的值。当存在子类型，你甚至可以有一个超类型存储属性和子类计算，反之亦然。但是，如果要使用动态属性，则只能更改存储的数据一个计算就是在通用访问器中为`动态属性`设置一个特定的数值,清单4中的代码。这个代码可能很脆弱，难以维护。</span>](#32 "Another key disadvantage of flexible dynamic properties is that it is difficult to substitute them for operations. One of the key advantages of encapsulation is that a client that uses a property cannot tell whether it is stored as part of an object’s data, or computed by a method. This is a very important part of the object approach. It allows you not just a regular interface for both purposes, but also to change your mind without the client knowing. In the presence of subtyping you can even have a supertype store the property and subclasses compute or vice versa. However if you want to use dynamic properties the only way you can change stored data to a calculation is to put a specific trap in the general accessor for the dynamic property along the lines of Listing 4. This code is likely to be brittle and awkward to maintain.")

```java
class Person {
    public Object getValueOf (String key) {
        if (key = “vacationAddress”) 
            return calculatedVacationAddress();
        if (key = “vacationPhone”) 
            return getVacationPhone();
        // else return stored value…
```
#### 列举4,用操作替换`动态属性`

- [<span id="33">其他形式的动态属性可以帮助您解决其中一些问题，但不是全部。该`动态属性`的最大的缺点是：你失去了清晰的接口和所有的设计时间检查。`动态属性`的不同方法会让你额外写不同的检查方法。如果你需要`动态属性`，并且当然有确定的情况你这样做，那么你只需要放弃设计时间检查和明确的设计时间接口。唯一的问题是如何明确接口和有多少运行时检查。使用灵活的动态属性也会有同样的问题。</span>](#33 "Other forms of dynamic property help you solve some of these problems but not all. The essential disadvantage of a dynamic property is that you lose the clear interface and all designtime checking. Different approaches to dynamic properties give you different abilities to do run-time checking. If you need dynamic properties, and there are certainly situations when you do, then you just have to give up design time checking and a explicit design time interface. The only question is how explicit an interface and how much checking you can do at run time. With Flexible Dynamic Properties you don’t get any of either.")

- [<span id="34">你经常在数据库中发现动态属性，因为改变它通常是一个痛苦数据库模式，特别是如果有大量的数据迁移。分布式的接口例如在`CORBA`中的组件也经常因为相似的原因而使用动态属性。那里是很多使用界面的远程客户，所以你不愿意改变它。在这两种情况下，编译时和运行时间之间的区别并不是设计时和生产之间的区别。</span>](#34 "You find dynamic properties often in databases because it is often a pain to change the database schema, especially if there would be a lot of data to migrate. Interfaces of distributed components, such as in CORBA, also often use dynamic properties for a similar reason. There are a lot of distant clients using the interface, so you are reluctant to change it. In both of these cases it is not so much a distinction between compile-time and run-time, as much as a distinction between design-time and production.") 

- [<span id="35">如果你正在做的是通过`GUI`显示和更新信息，而代码永远不会对键进行固定的引用（即，你永远不会看到像清单3那样的代码），那么使用灵活`动态属性`就非常安全。这是因为你没有设置一个任意字符串作为一个关键的讨厌的依赖。 否则，你应该考虑`动态属性`的其他方法之一。</span>](#35 "If all you are doing is displaying and updating information via a GUI, and the code never makes a fixed reference to the keys (i.e. you never see code like Listing 3), then you are pretty safe with a Flexible Dynamic Property. This is because you have not set up a nasty dependency to some arbitrary string as a key. Otherwise you should consider one of the other approaches to dynamic properties.")

- [<span id="36">更多运行时检查的第一步是定义的动态属性。与`灵活动态属性`相反，定义的关键区别在于`动态属性`使用的关键字不再是一些任意的字符串，而是现在某个类的一个实例（图3）。</span>](#36 "The first step towards more run-time checking is the Defined Dynamic Property. The key difference between a defined as opposed to a flexible dynamic property is that the key used by the dynamic property is no longer some arbitrary string, but is now an instance of some class (Figure 3).")

![image](https://static.zuul.top/java-design-patterns-doc-for-cn/abstract-document/7_1.png)

#### 图3.定义的`动态属性`

- [<span id="37">在它的表面上使用定义的`动态属性`并没有太大的改变。事实上，代码界面几乎完全相同（清单5和清单6）。但是现在，关键字的选择不再是完全随意的，而是受到接触`类型`的限制。当然，这仍然允许您在运行时添加`属性`-只需创建一个新的关联`类型`。不过现在至少在某个地方可以找到一个潜在的`键`列表，而无需浏览程序`代码`。 在设计时添加的任何键都可以在关联类型类的加载程序中收集。您可以轻松地提供服务，以在运行时查找合法的`键`。</span>](#37 "On the face of it using defined dynamic property does not change much. Indeed the code interface is almost identical (Listing 5 and Listing 6). But now the choice of keys is no longer entirely arbitrary, it is limited by the instances of contact type. Of course this still allows you to add properties at run time – you just create a new contact type. However now there is at least somewhere someone can look to get a list of potential keys without having to trawl through the program text. Any keys added at design time can be collected in a loader routine in the contact type class. You can easily provide services to find out the legal keys at run time.")

```java
class Person {
    public Object getValueOf(ContactType key);
    public void setValueOf(ContactType key, Object value);
```
#### 列举5, 图3的Java接口
```java
class ContactType {
    public static Enumeration instances();
    public static boolean hasInstanceNamed(String name);
    public static ContactType get(String name);
```
#### 列举6,为定义的属性类型提供的服务

- [<span id="38">你现在可以设置一些检查来防止由于某人要求一个不存在的`动态属性`而导致的错误。我在这里抛出一个未经检查的`异常`，因为我认为`get（）`的前提条件是`客户端`为联系人类型提供合法名称。客户端总是可以通过使用`hasInstanceNamed（）`来执行这个检查，但是大多数情况下客户端使用的是类型而不是字符串。</span>](#38 "In particular you can now set up some checking to prevent errors due to someone asking for a dynamic property that does not exist as in Listing 7. I’m throwing an unchecked exception here because I consider that the precondition for get() is that the client provides a legal name for a contact type. The client can always fulfill this responsibility by using hasInstanceNamed(), but most of the time client software will hang on to contact type objects, not strings.")

---

<h3 align = "center">定义动态属性</h3>
- [<span id="39">你如何代表一个对象的事实？</span>](#39 "How do you represent a fact about an object?")
- [<span id="39">提供用某种类型的实例参数化的属性。声明一个属性创建一个新类型的实例</span>](#39 "Provide an attribute parameterized with an instance of some type. To declare a property create a new instance of that type") 

---

- [<span id="40">通常，联系人类型将保存在字典中，通常由字符串索引。这个字典可能是一个静态的联系人类型的字段，但是我更愿意把它作为注册服务器上的字段。</span>](#40 "Usually the contact types will be held in a dictionary, usually indexed by a string. This dictionary could be a static field of contact type, but I prefer to make it a field on a Registrar.")

- [<span id="41">删除联系人类型仍然具有尴尬的后果。在`java`中的`动态属性`仍然会出现在那些拥有它们的对象上，除非你写了一些复杂的东西清理代码。我通常会规定永远不要删除动态属性的键。如果你想使用一个新的名字，你可以通过给它一个其他名字，但是把它放置在定义的字典中几次，很容易地为联系类型添加别名。</span>](#41 "Removing a contact type still has awkward consequences. In java the dynamic properties would still be present on those objects that had them, unless you write some complicated clean up code. I usually make it a rule to never delete the keys for a Defined Dynamic Property. If you want to use a new name you can easily alias the contact type by giving it one name but placing it in the defining dictionary several times.")

```java
class ContactType {
    public static ContactType get(String name) {
        if (! hasInstanceNamed (name)) throw new IllegalArgumentException(“No such contact type);
        // return the contact type
}
// use with
Address kentVactation = (Address)kent.getValueOf(ContactType.get(“VacationAddress”));
```
#### 列举7, 检查使用合法合同类型

- [<span id="42">在这一点上，您可能想知道这与概念建模有什么关系，毕竟我写了很多代码并讨论了设计的权衡。这是一个重要的概念问题，因为您所做的概念选择会影响您的实现选择。如果你选择在你的概念模型中使用`灵活动态属性`，你很难在你的实现中使用定义的`动态属性`或`固定属性`。你做概念模型的原因之一是探索你的用户的概念是什么固定的，什么是可变的。如果全面的灵活性是我唯一的目标，那么我会总是使用图4.通过这个，我可以模拟世界上的任何情况。但是这个模型不是很有用。它在现实项目中是没用的，它不表示什么是固定的。什么时候你正在做一个概念模型，你需要知道你的选择如何影响项目实施-否则你失去了作为建模者的作用。</span>](#42 "At this point you might be wondering about what this has to do with conceptual modeling,after all I am writing a lot of code and discussing design trade-offs. This is an important conceptual issue because the conceptual choice you make affects the implementation options you have. If you choose to use flexible dynamic attributes in your conceptual model, you are making it pretty hard to use either defined dynamic attributes or fixed attributes in your implementation. One of the reasons you do conceptual models is to explore what is fixed and what is changeable in your users’ concepts. If total flexibility was my only goal then I would always use Figure 4. With this I can model any situation in the world. But this model is not very useful. Its uselessness comes from the fact that it does not indicate what is fixed. When you are doing a conceptual model you need to be aware of how your choices affect things in implementation – otherwise you are abdicating your responsibility as a modeler.")

- [<span id="43">我经常发现人们发现`动态属性`，然后想要在任何地方使用它们。灵活性如此之大，他们获得了所有的可扩展性。是的，有时候你需要`动态属性`。但永远不会忘记有一个标准。只有当你真的使用它们需要他们才用。毕竟，如果必须使用，以后很容易添加它们。</span>](#43 "I often find that people discover dynamic properties, and then want to use them everywhere. The flexibility is so great, they get all the extendibility they ever want. Yes sometimes you need dynamic properties. but never forget there is a price. Only use them when you really need them. After all it is easy to add them later if you have to.")

![image](https://static.zuul.top/java-design-patterns-doc-for-cn/abstract-document/8_1.png)
#### 图4.一个可以无用建模任何域的模型

- [<span id="44">`定义动态属性`允许您更多地指出你拥有的属性。这些属性仍然是无类型的。您不能强制图3中休假地址的值是一个地址。 你可以通过使用`类型动态属性`来做些什么。</span>](#44 "The Defined Dynamic Property allows you to indicate rather more about what properties you have. These properties are still untyped. You cannot enforce that the value of the vacation address in Figure 3 is an address. You can do something about that by using a Typed Dynamic Property.")

![image](https://static.zuul.top/java-design-patterns-doc-for-cn/abstract-document/9_1.png)
#### 图5.为使用限定关联的类型化动态属性建模

- [<span id="45">`类型动态属性`将类型信息添加到定义的`动态属性`（图6和6）图5）。这里的联系人类型的实例不只是指出该人是什么合适的人有，他们也表示每个`属性`的类型。 类型约束的值，沿线清单9。</span>](#45 "A typed dynamic property adds type information to the defined dynamic property (Figure 6 and Figure 5 ). Here the instances of contact type do not just indicate what properites the person has, they also indicate the type of each property. The type constrains the value, along the lines of Listing 9.")

```java
class Person {
    public Object getValueOf(ContactType key);
    public void setValueOf(ContactType key, Object value);
class ContactType {
    public Class getValueType();
    public ContactType (String name, Class valueType);
```
#### 列举8, 键入动态属性的操作

```java
class Person {
    public void setValueOf(ContactType key, Object value) {
        if (! key.getValueType().isInstance(value))
            throw IllegalArgumentException (“Incorrect type for property”);
        // set the value
```
#### 列举9, 做类型检查

- [<span id="46">这样做类型检查可以帮助避免错误，但它仍然不像固定属性那样清晰。 检查是在运行时，而不是在设计时，因此不是有效的。但还是比没有检查好，特别是如果你习惯于强类型的环境时。</span>](#46 "Doing type checking like this can help to avoid errors, but it still is not as clear as fixed properties. The checking is at run time, not at design time, and is therefore not as effective. Still it is better than no checking at all, particularly if you are used to a strongly typed environment.")

---
<h3 align = "center">类型动态属性</h3>
- [<span id="47">你如何代表一个对象的事实？</span>](#47 "How do you represent a fact about an object?")</br>
- [<span id="47">提供使用某种类型的实例进行参数化的属性。声明一个属性创建一个新类型的实例并指定值的类型属性。</span>](#47 "")
---

- [<span id="48">当我们深入研究`动态属性`时，我们会发现更丰富的`反射`示例，这是一种架构模式，当我们获得能够描述自身的运行时对象时，就会出现这种模式。 \[POSA\]比我打算在这里更详细地讨论反思。</span>](#48 "As we delve deeper into dynamic properties, we find richer examples of reflection, an architectural pattern which appears when we get runtime objects that are able to describe themselves. [POSA] discusses reflection in much more detail than I intend to go into here.")

- [<span id="49">动态属性提供反射功能，即使在那些不支持反射的语言中。即使使用了一种能够提供一些反射的语言，`动态属性`的反射也更加集中 - 所以您可以提供更易于使用的接口。</span>](#49 "Dynamic properties provide a reflective capability, even in those languages that don’t support reflection themselves. Even with a language that does provide some reflection, the reflection of dynamic properties is more focused – so you can provide an easier to use interface.")

- [<span id="50">使用所有这些合格的关联可能会很难遵循。另一种方式提供`类型动态属性`是使用单独的属性模式。独立属性模式的本质是它使属性成为一个对象（图6和清单10）。 你可以获得一个人的属性，然后与每个属性获得值和类型信息。</span>](#50 "Using all of those qualified associations can get rather hard to follow. Another way of providing typed dynamic properties is to use the separate property pattern. The essence of the separate property pattern is that it makes the property an object in its own right (Figure 6 and Listing 10). You can get hold of the properties of a person, and then with each property get value and type information.")


---
<h3 align = "center">分离属性</h3>
- [<span id="51">你如何代表一个对象的属性，并允许属性记录这个属性<span>](#51 "How do you represent a fact about an object, and allow facts to be recorded about that fact")
- [<span id="51">为每个属性创建一个单独的对象。有关该属性的子属性可以然后被做成那个对象的属性。<span>](#51 "Create a separate object for each property. Facts about that property can then be made properties of that object.")
---

- [<span id="52">`独立属性`和限定的关联`动态属性`总是可用的两种选择。 到目前为止，我已经用限定的关联描述了灵活的和定义好的`动态属性`，因为合格的关联提供了一个更容易使用的接口。如果你愿意的话，你可以使用灵活和定义的具有单独属性的`动态属性`，尽管我不打算进入在这里。当我们了解类型化`动态属性`的复杂性时，`分离属性`风格变得更有优势。<span>](#52 "Separate properties and qualified associations are two alternatives that are always available for dynamic properties. So far I’ve described flexible and defined dynamic properties with qualified associations because the qualified association presents a much easier interface to use.You can use flexible and defined dynamic properties with separate properties if you wish, although I’m not going to go into that here. As we get to the complexity of typed dynamic properties and onwards the separate property style becomes more of an advantage.")

![image](https://static.zuul.top/java-design-patterns-doc-for-cn/abstract-document/10_1.png)
#### 图6.为分类的动态属性建模，使用单独的属性

```java
class Person {
    public Enumeration getProperties();
class ContactProperty {
    public Object getValue();
    public Class getType();
    public ContactType getIndex();
```
#### 列举10, 使用单独属性的类型化动态属性的操作

- [<span id="53">`分离属性`和有限的关联不是相互排斥的。您可以轻松地同时提供两个接口。 这样你就得到了两者的优点。当然这会使接口更加复杂，所以先考虑一下用户的需求。给他们提供他们需要的接口，不要让接口变得复杂。但是，如果他们需要合格的关联和`分离属性`，那么这是一个合理的选择。我通常会使用合格的关联来获得值，但是这种类型可能没有多大意义。<span>](#52 "Separate properties and qualified associations are not mutually exclusive. You can easily provide both interfaces at the same time. This way you get the advantages of both. Of course that makes the interface more complex, so think first about what the clients of person need.Give them the interface they need, don’t make it over complex. But if they need both qualified associations and separate properties, then that is a reasonable option. I would normally always use qualified associations for the value, but it may not make as much sense for the type.")

- [<span id="54">您也可以在这里考虑接口/实现的差异。在本文中，我想集中在概念上 - 它映射到软件的接口而不是实现。但值得一提的是，您可以在实现中使用单独的对象时提供合格的关联接口。如果人的客户端可以获取联系人属性对象，则只能在接口中使用单独的属性。通常隐藏`分离属性`以简化客户端的接口是有用的。</span>](# "You can also consider the interface/implementation differences here. In this paper I want to concentrate on the conceptual – which maps to the interface of software rather than its implementation. But it is worth mentioning that you can provide a qualified association interface while using separate object in the implementation. You are only using separate properties in the interface if a client of person can obtain a contact property object. Often it is useful to hide the separate property to simplify the interface for the client.")

- [<span id="55">`分离属性`的一大优势是它可以让你把属性的信息放在属性中。 这些信息可能包括谁确定了属性，什么时候确定了属性等。 \[Fowler AP§3.5\]中的观察模式基于这个主题进行了深入的研究。如果您需要单独的属性，我在观察者模式所描述的大部分内容都值得思考。（我将观察模式看作是使用不同的属性。）</span>](#55 "One of the big advantages of the Separate Properties is that it allows you put information about the property in the property. Such information might include who determined the property, when it was determined, and the like. The Observation pattern in \[Fowler AP §3.5\] build upon this theme in some depth. Much of what I’ve described there in terms of observations is worth considering if you need separate properties. \(I see the observation pattern as a use of separate properties.\)")

- [<span id="56">您可能想知道`分离属性`（模式）和限定关联（`UML`建模结构）之间的对比。 你也可以把合格的关联看作一种模式，一种联想模式。确实，我在\[Fowler AP §15.2\]中做了这个。我发现为设计创建模型考虑是有帮助的，因为它帮助我思考使用它们的权衡。当你将它们的模型比较清楚，如`分离属性`，这是特别有用的。当然，以模式开始的事情可以转化为建模结构，特别是如果使用`UML`构造型。历史映射模式\[FowlerAP§15.3\]就是一个很好的例子。我表示使用这种模式非常刻版。这是一个模式或建模？也许这是一个地板蜡和一个沙漠顶部。</span>](#56 "You might be wondering at the contrast between separate properties \(a pattern\) and qualified associations \(a UML modeling construct\). You can also think of qualified associations as a pattern, a pattern of association. Indeed I did do this in \[Fowler AP §15.2\]. I have found it helpful to think of modeling constructs as patterns, for it helps me think about the trade-offs in using them. This is particularly useful when you are comparing them to something that is more clearly a pattern, such as separate property. Of course things that begin as patterns can be turned into modeling constructs, particularly if you use UML stereotypes. The historic mapping pattern \[Fowler AP §15.3\] is a good example of that. I represent that using the «history» stereotype. Is it a pattern or a modeling construction? Maybe it’s a floor wax and a desert topping too.")

---
## [<span id="57">具有多值关联的动态属性</span>](#57 "Dynamic Properties with Multi-valued associations")

- [<span id="58">我上面的例子集中讨论了`动态属性`中每个键都有一个单一值的情况。 但是，您也可以在`动态属性`中有多个事件的情况。与人相处时，你可能会考虑一个多值的友好属性。处理这个问题有两种方法，一种简单而不令人满意，另一种令人满意，但（太）复杂。</span>](#58 "My examples above have concentrated on cases where there is a single value for each key in the dynamic properties. But you can also have cases where there are multiple items in the dynamic properties. With Person you might consider a friends property which is multi-valued.There are two ways to deal with this, one that is simple and unsatisfying, another that is satisfying but (too) complex.")


- [<span id="59">简单的方法就是说`动态属性`的值可以是一个集合。然后我们可以像使用相同接口的其他对象一样操作它（清单11）。这很好，很简单，因为我们不需要对基本的`动态属性`模式做任何事情（这里的例子是一个类型化的`动态属性`，但是它可以和所有的模式一起工作）。然而，这并不令人满意，因为它不是真的是我们想要处理多值属性的方式。如果朋友是一个固定的属性，我们需要一个接口，如清单12所示。我不喜欢在这些情况下暴露集合。通过这样做，人员班级在我们添加或移除元素时就失去了应对的能力。这也消除了我们改变我们正在使用的集合类型的能力。</span>](#59 "The simple approach is just to say that the value of a dynamic property can be a collection.We can then manipulate it like any other object with the same interface (Listing 11). This is nice and simple, since we don’t have to do anything to the basic dynamic property pattern.(The example here is with a typed dynamic property, but it will work with all of them.) It’s unsatisfying however because it is not really the way we would like to deal with multi-valued properties. If friends were a fixed property, we would want an interface along the lines of Listing 12. I don’t like exposing the vector in these cases. By doing so the person class loses the ability to react when we add or remove elements. It also removes our ability to change the type of collection we are using.")

```java
Person aPerson = new Person();
ContactType friends = new ContactType(“Friends”, Class.forName(“Vector”));
Person martin = new Person(“Martin”);
martin.setValueOf(“Friends”, new Vector());
Person kent = new Person(“Kent”);
martin.getValueOf(“Friends”).addElement(“Kent”);
Enumeration friends = martin.getValueOf(“Friends”).elements();
```
#### 列举11, 在类型化动态属性中使用集合值
```java
class Person {
    public Enumeration getFriends();
    public void addFriend(Person arg);
    public void removeFriend(Person arg);
```
#### 列举12, 一个固定的多值属性的运作

- [<span id="60">那么当我们有`动态属性`的时候，我们可以按照清单12的方式获得一个接口吗？ 那么，如果我们努力工作，就可以如图7所示。但这是一个复杂的模型。 通过一些巧妙的编码，我们可以隐藏接口（清单13和清单14）背后的大部分复杂性，并且使用起来相当方便（清单15）。但客户端仍然需要知道哪些属性是单值的，哪些属性是多值的，并且只有在运行时才能检查正确的使用情况。所有这些复杂性都是痛苦的-比使用`固定属性`更痛苦。我会非常不愿走这么远。</span>](#60 "So can we get an interface along the lines of Listing 12, when we have dynamic properties? Well if we try hard enough we can, as you can see in Figure 7. But it is a complex model. With some clever coding we can hide much of that complexity behind the interface (Listing 13 and Listing 14) and make it reasonably convenient to use (Listing 15). But the client still needs to know which properties are single valued and which are multi-valued and all the checking for the right usage can only occur at run time. All this complexity is painful – a lot more painful than using fixed properties. I would be very reluctant to go this far.")

![image](https://static.zuul.top/java-design-patterns-doc-for-cn/abstract-document/12_1.png)

#### 图7.满足对多值动态属性的过度支持

```
class Person
    public Object getValueOf(ContactType key);
    public Enumeration getValuesOf(ContactType key);
    public void setValueOf(ContactType key, Object newValue);
    public void addValueTo(ContactType key, Object newValue);
    public void removeValueFrom(ContactType key, Object newValue);
    
class ContactType
    public Class getValueType();
    public boolean isMultiValued();
    public boolean isSingleValued();
    public ContactType(String name, Class valueType, boolean isMultiValued);
```
#### 列举13, 图7的操作

```java
class Person
    public Object getValueOf(ContactType key) {
        if (key.isMultiValued())
            throw IllegalArgumentException(“should use getValuesOf()”)
        //return the value
    }
    
    public void addValueTo(ContactType key, Object newValue) {
        if (key.isSingleValued())
            throw IllegalArgumentException(“should use setValueOf”);
        if (! key.getValueType().isInstance(newValue))
            throw IllegalArgumentException (“Incorrect type for property”);
        //add the value to the collection
```
#### 列举14, 检查清单13的操作的使用情况

```java
fax = new ContactType(“fax”, Class.forName(“PhoneNumber”), false);
Person martin = new Person(“martin”);
martin.setValueOf(“fax”, new PhoneNumber(“123 1234”);
martinFax = martin.getValueOf(“fax”);
friends = new ContactType (“friends”, Class.forName(“Person”), true);
martin.addValueTo(“friends”, new Person(“Kent”));
```
#### 列举15, 使用清单13的操作

- [<span id="61">这种复杂性似乎是因为我们既有多值也有单值的`属性`。处理这些复杂性有一个内在的不同的接口，因此复杂性也是如此。当然，我们可以得到只有多值属性的情况。一个常见的模式是类型关系模式（图8）。在这里，一个人可能与许多不同公司有不同的雇佣关系（甚至与同一家公司有多个）。</span>](#61 "This complexity appears because we have both multi valued and single-valued properties.There is an inherently different interface to dealing with these, hence the complexity. Of course we can get situations with only multi-valued properties. A common pattern for this is the Typed Relation ship pattern \(Figure 8\). Here a person may have number of different employment relationships with a number of different companies \(or even several with the same company\).")

![image](https://static.zuul.top/java-design-patterns-doc-for-cn/abstract-document/13_1.png)
#### 图8.类型关系的一个例子

```java
class Employment {
    public Employment (Person person, Company company, Employment Type type);
    public void terminate()
    …
}
class Person {
    public Enumeration getEmployments();
    public void addEmployment (Company company, EmploymentType type);
```
#### 列举16, 图8的`Java`接口

- [<span id="62">正如我们想到的那样，很快就会发现，这与使用多值的`定义动态属性`非常类似，但是使用`分离属性`而不是合适的关联来表示。（或者说这句话太过分了？）实际上，图9显示了在这种情况下如何使用`定义动态属性`接口。这种事物的观点是真实的，所以一个类型化的关系不会添加任何新的模式语言。 但是类型化关系在建模圈子中是一种非常普遍的模式，很多人可能没有意识到它与`动态属性`模式的联系。</span>](#62 "As we think of this, it should soon occur to you that this is really very similar as using a Defined Dynamic Property that is multi-valued, but expressed using a Separate Property rather than a Qualified Association. (Or is that sentence just too much of a mouthful?) Indeed Figure 9 shows how you can use a Defined Dynamic Property interface in this situation. This view of things is true, and so a typed relationship doesn’t add anything that new to this pattern language. But typed relationship is a very common pattern in modeling circles, and many may not realize its connection with the dynamic properties patterns.")

---
<h3 align = "center">类型关系</h3>
- [<span id="63">你如何表示两个对象之间的关系？（你如何表示多值动态属性？）</span>](#63 "How do you represent a relationship between two objects?(How do you represent multi-valued dynamic properties?)")
- [<span id="63">为两个对象之间的每个链接创建一个关系对象。 给关系对象一个类型对象来表示关系的含义。（类型对象是多值属性的名称。）</span>](#63 "Create a relationship object for each link between the two objects. Give the relationship object a type object to indicate the meaning of the relationship.(The type object is the name of the multi-valued property.)")
---

- [<span id="64">类型化关系的优势在于它可以很好地处理双向关系，并且为关系添加属性提供了一个简单的点。（当然，后者是一个`分离属性`的特征。）你可以在这个模式中添加一个复杂的知识级别，跟类型化的`动态属性`一样。但是，您应该考虑接口的影响。类型化关系迫使用户意识到雇佣对象，因为确实使用`分离属性`。事实上，人们倾向于将属性客体本身看作完全成熟的客体，而不是人（或公司）的一些属性。 但是合格的关联通常可以为许多目的提供更简单的接口。所以每当你看到，或者你正在考虑使用，一个类型的关系;你还应该考虑合格的关联形式。您可以在任何一个方向或两个方向上使用它，也可以将其用于除了键入的关系之外，或者除此之外。。</span>](#64 "The strengths of typed relationship are that it works well with bi-directional relationships, and that it provides a simple point to add properties to the relationship. (The latter, of course, is a feature of separate properties.) You can add a sophisticated knowledge level to this pattern,along much the same lines as typed dynamic properties. However you should consider the interface implications. Typed relationships force users to be aware of the employment object,as indeed does any use of separate properties. Indeed people tend to see the property object as a full fledged object in its own right, rather as some property of the person (or company). But the qualified association can often provide a simpler interface for many purposes. So whenever you see, or you are considering using, a typed relationship; you should also consider the qualified association form. You can use it in either or both directions, and use it either in addition to the typed relationship, or in addition to it.")

- [<span id="65">但是这两种模式并不完全相同。如果使用图9，则表示雇主只能是某种特定工种的雇主。图8在图表中没有这样的约束，尽管大多数建模者会暗示这样的约束，除非雇用具有附加属性。当然，就业通常具有附加属性。一个常见的例子是日期范围（如问责制\[Fowler，AP§2.4\]）。</span>](#65 "The two models are not quite identical however. If you use Figure 9 you are indicating that an employer can only be an employer once for a particular employment type. Figure 8 has no such constraint in the diagram as it stands, although most modelers would imply such a constraint,unless the employment had additional attributes. Often, of course, the employment does have the additional attributes. A common example is a date range (as in accountability \[Fowler, AP §2.4\].")

![image](https://static.zuul.top/java-design-patterns-doc-for-cn/abstract-document/14_1.png)
#### 图9.使用与图8相同情况的合格关联

```java
public Person {
    public void addEmployer (Company company, EmploymentType type);
    public Enumeration getEmployersOfType (EmploymentType type);
```
#### 列举17, 图9的接口

![image](https://static.zuul.top/java-design-patterns-doc-for-cn/abstract-document/15_1.png)
#### 图10.键入的关系，显示通常假定的约束

---
## 不同种类的人
- [<span id="66">到目前为止，我们假设我们只有一种人，我们为一个人定义的任何属性都是所有人的有效属性。但是，您确实会遇到不同类型的情况，以及不同类型的不同属性。管理人员可能需要一个管理部门的属性，执行人员可能需要一个属性作为高管卫生间的关键号码（在一个不是90年代的公司）。</span>](# "So far we are assuming we only have one kind of person, and any properties we define for a person are valid properties for all people. However you do get situations where you have different types, and different properties for different types. A manager may need a property for department managed, an executive may need a property for executive washroom key number (in a not very 90’s company).")

- [<span id="67">别担心，我听到“使用继承愚蠢”的呼声。事实上，这是常用于分类的情况之一。实际上，这个过程比这个要复杂得多，特别是当你开始思考一个人可能扮演的角色时。我已经写了关于建模角色\[Fowler roles\]的主题的全文。角色模式考虑了我们对操作变化和`固定属性`变化感兴趣的情况。但在这种情况下，我想探索不同类型的对象与`动态属性`的概念的重叠。这种重叠会导致`动态属性知识级别模式`（一个对我的品味有点太大的名字）。</span>](#67 "Don’t worry, I hear the cries of “use inheritance stupid”. Indeed this is one of the situations that is often used for subtyping. Actually it gets rather more involved than that, particularly when you start thinking of the various roles a person may play. I’ve written a whole paper on the subject of modeling roles \[Fowler roles\]. The roles patterns consider cases where we are interested in variations in operations and in variations of fixed properties. But in this case I want to explore the overlap of different kinds of object with the notion of dynamic properties. This overlap begets the dynamic properties knowledge level pattern \(a name that is getting a little too large for my taste\).")

- [<span id="68">为了使用这个模式，我们给`Person`一个`Person`类型的`类型对象`。然后，我们可以说，人物类型与联系人类型的关联指示哪些人物拥有该人物类型可用的属性。 如果我们尝试使用或要求某人的属性，则可以使用人员类型来检查使用情况是否正确。</span>](#68 "To use the pattern we give the Person a type object of Person Type. We can then say that the person type’s association to contact type indicates which properties are available for people who have that person type. If we try to use, or ask for, a property on a person the person type can be used to check that the usage is correct.")

![image](https://static.zuul.top/java-design-patterns-doc-for-cn/abstract-document/16_1.png)
#### 图11.动态财产知识水平

```java
class Person {
    public Object getValueOf(ContactProperty key);
    public boolean hasProperty(ContactProperty key);
    public void setValueOf(ContactProperty key, Object newValue);
class PersonType {
    public boolean hasProperty(ContactProperty key);
    public Enumeration getProperties();
```
#### 列举18, 图11的操作
```java
class Person {
    public Object getValueOf (ContactProperty key) {
        if (!hasProperty(key))
            throw IllegalArgumentException(“Innapropriate key”);
            //return the value
```
> 列举19, 检查具有动态属性知识级别的适当的密钥

- [<span id="69">当我们开始使用这样的知识水平时，单独的属性变得越来越重要。 在这种情况下，我们很快就会开始停止将其视为一种属性，而不是把它作为一个对象。 什么是属性和什么是非属性之间的分界线是非常模糊的，这实际上取决于你对事物的看法。</span>](#69 "As we start to use a knowledge level like this, the separate property becomes more and more important. In this case we soon start to stop thinking of it as a property, rather as some object in its own right. The dividing line between what is a property and what isn’t is very blurred,and it really depends upon your view of things.")

---
<h3 align = "center">动态属性知识水平</h3>
- [<span id="70">你如何执行某些类型的对象具有某些特性使用动态属性？</span>](#70 "How do you enforce that certain kinds of objects have certain properties when you use dynamic properties?")
- [<span id="70">创建一个知识级别来包含什么类型的对象使用的规则哪些类型的属性</span>](#70 "Create a knowledge level to contain the rules of what types of objects use which types of properties")
---

---

## [<span id="71">动态属性的几个小结</span>](#71 "Some Summary Points on Dynamic Properties")

- [<span id="72">各种各样的`动态属性`构成了本文的大部分内容。但我必须重申，`动态属性`是我想要尽可能避免的。`动态属性`带来了很大的负担：接口不够清晰，使用操作而不是存储数据的困难。只是有时你别无选择，只能使用它们，在这种情况下，这篇论文应该有用的给你提供一些替代方案和之间的权衡。<span>](#72 "Various kinds of dynamic properties make up the bulk of this paper. But I have to reiterate that dynamic properties are something I like to avoid if at all possible. Dynamic properties carry a heavy burden of disadvantage: the lack of clarity of the interface, the difficulty in using operations instead of stored data. It is just that sometimes you have little choice but to use them, and it is on these occasions that this paper should come in useful to give you some alternatives and the trade-offs between then.")

- [<span id="73">`动态属性`出现在改变接口有困难的地方。那些使用像他们这样的分布式对象系统的人，至少在原则上是这样，因为它允许他们在不改变客户端的情况下改变接口 - 而在分布式系统中，可能很难找到你的客户端。但是你仍然应该警惕这样做。每当你为`动态属性`添加一个新的键到你的键上，你都在有效地改变接口。所有的`动态属性`都在替换运行时检查的编译时间检查。你仍然有同样的问题保持你的客户端最新。</span>](#73 "Dynamic properties appear most where there are difficulties in changing the interface. People who work with distributed object systems like them, at least in principle, because it allows them to alter an interface without compromising clients – and in a distributed system it may be very difficult to find who your clients are. But you should still be wary of doing this. Any time you add a new key to your keys for the dynamic properties you are effectively changing the interface. All the dynamic properties are doing is replacing a compile time check for a runtime check. You still have the same issues of keeping your clients up to date.")

- [<span id="74">`动态属性`的另一个常见用途是在数据库中。这里不仅仅是由于接口的问题，而且由于数据迁移的问题（如果不是主要的话）。更改数据库模式不仅会导致对使用该模式的程序进行潜在更改，还可能会强制您执行复杂的数据转换练习。同样，`动态属性`允许您在不更改数据库模式的情况下更改内容，从而不需要进行任何数据转换。在大型数据库中，这可能是一个引人注目的优势。</span>](#74 "Another common use of dynamic properties is in databases. Here it is not just due to the problem of interface, but also (if not primarily) due to problems of data migration. Changing a database schema does not only cause a potential change to programs using the schema, it also may force you to do a complicated data conversion exercise. Again dynamic properties allow you to change things without changing the database schema, and thus not needing to do any data conversion. In large databases this can be a compelling advantage.")

---

## [<span id="75">一个你不知道的有关于属性的](#75 "A property you don’t know about")

- [<span id="76">我想在本文中添加一个最后一个重要的属性。这是一个没有意识到属性的对象的情况。当属性被另一个对象所隐含，以及与有关的方式时，就会发生这种情况。</span>](#76 "There is a last but important kind of property that I want to add to this paper. This is the case of an object having a property without realizing it. This occurs when the property is implied by another object and the way it relates to you.")

- [<span id="77">考虑一个管理数据库连接的对象。它会创建一堆数据库连接，并在请求时将它们传递给其他对象。当一个客户端连接完成后，可以将其返回给管理员，以供其他人使用。您可以通过向连接添加`isBusy`属性来完成此操作。图12显示了一个使用外部属性的替代方案。连接是空闲的还是繁忙的是由连接管理器中的哪个集合决定的。如果你有一个连接，你不能问它是空闲的还是忙的，而是你必须要求连接管理器是否特定的连接空闲或忙碌。你可以这样说，因为组合关联是一种方式。连接不知道连接管理器。 从某种意义上来说，空闲/忙碌状态根本不是连接的属性。但至少从某种意义上来说，这就是我提到它的原因。</span>](#77 "Consider an object that manages database connections. It creates a bunch of database connections and hands them out to other objects when requested. When a client is done with the connection it can return it to the manager to be available for someone else. You could do this by adding an isBusy property to the connection. Figure 12 shows an alternative using an extrinsic property. Whether the connection is free or busy is determined by which collection in the connection manager it lies in. If you had a connection, you could not ask it whether it is free or busy, instead you would have to ask the connection manager whether a particular connection is free or busy. You can tell this because the composition associations are one way.The connection has no knowledge of the connection manager. In a sense the free/busy status isn’t a property of connection at all. Yet at least in some sense it is, which is why I mention it.")

![image](https://static.zuul.top/java-design-patterns-doc-for-cn/abstract-document/17_1.png)
#### 图12.使用外部收集属性

- [<span id="78">在纯粹的概念模型意义上，这种模式没有多大意义。但是，为什么你可能想要使用它，有实际的实施原因。如果您希望对此属性进行的所有更改都通过连接管理器进行，则此方法可以清楚地说明这一点。特别是当你想让连接管理器给你一个自由的连接，而你不关心哪一个时，这是一种自然的风格。</span>](#78 "In a pure conceptual modeling sense this pattern does not make much sense. But there are practical implementation reasons why you may want to use it. If you want all changes to this property to go through a connection manager, then this approach makes this clear. In particular this is a natural style when you want the connection manager to give you a free connection and you don’t care which one.")。

- [<span id="79">使用外部属性的另一个原因是如果连接类是由其他人提供的，并且您不能更改其接口。 你可以添加新的属性而不用改变连接类。</span>](#79 "Another reason to use an extrinsic property is if the connection class is provided by someone else and you can’t change its interface. You can add the new property without changing the connection class at all.")

---
外在属性
- [<span id="80">你如何给对象一个属性而不改变它的接口？</span>](#80 "How do you give an object a property without changing its interface?")
- [<span id="80">让另一个对象负责知道这个属性。</span>](#80 "Make another object responsible for knowing about the property.")
---

- [<span id="81">`外在属性`的一个大问题是它会导致一个尴尬和不自然的接口。通常如果你想知道一些东西，你只要找到合适的对象并提出问题。在这里您需要找到保存外部集合的对象，并询问有关适当的对象。在某些情况下，比如这个，似乎是合理的。但大多数情况下，我宁愿让对象了解自己的属性（在这种情况下，我称之为`内在属性`）。</span>](#81 "The big problem with the extrinsic property is that it leads to an awkward and unnatural interface. Usually if you want to know something, you just find the appropriate object and ask it. Here you need to find the object that holds the external collection, and ask it about the appropriate object. In some circumstances, such as this one, it seems reasonable. But most of the time I would prefer to let objects know about their own properties (in which case I call them intrinsic properties).")

---

## 最后的想法

- [<span id="82">当我完成本文时，我觉得需要再次敦促你不要使用我在这里写的东西，除非你真的需要它。`固定属性`的好处是伟大的。如果你需要别的东西，那么我希望这篇文章能给你一些想法和一些指导。但`固定属性`永远是你的第一选择。</span>](#82 "As I finish this paper, I feel the need again to urge you not to use what I’ve been writing about here unless you really do need it. The advantages of fixed properties are great. If you need something else, then I hope this paper gives you some ideas and some guidance. But fixed properties are always your first choice.")

---

## 参考

- [Fowler, AP] Fowler, Martin. Analysis Patterns: Reusable Object Models, Addison-1997
- [Fowler, roles] Fowler, Martin. Dealing with Roles,http://www.awl.com/cseng/titles/89542-0/awweb.htm
- [POSA] Buschman et al, Pattern Oriented Software Architecture, Wiley 1997
