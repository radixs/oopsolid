[toc]

# Introduction
Programming is fun. But it can be also daunting and make you feel miserable if you have to scratch your head too often. It does not have to be that way, ever.

Those that maintain their code in a truly object oriented way and stick to some well established coding habits and conventions breathe easily. Their code is easy and convenient to maintain and
they can focus on adding new, cool features rather than trying to decipher *what this stuff does* all the time.

## The very beginnings, procedural *evolving* into static
When learning programming everybody has to start somewhere and we usually start with some tutorials that teach us basics like data types, how to use if statements and switches,
loops and some of the most useful functions offered by the language engine. We start with one project file, start out by printing ```Hello World``` and
end up with some more or less procedural script that does some simple stuff. And that's it. You are on your own now.

If you are not some lucky person who has the luxury of having somebody to guide you further and teach you modern programming techniques you will have to navigate the
web, read many, many more tutorials and visit [stackoverflow](http://stackoverflow.com) a few thousand times in order to step-by-step - learn new and more advanced things that will let you solve
the one particular problem you have at the moment. And you can definitely solve problems, one success after another, but when your projects grow and the number of scripts
grow you have one more problem to solve: how to manage it all? How to keep track of what happens where and when?

Eventually to solve that problem you will run into tools like frameworks and/or content management systems where you will do your best to use pre-built functions and try to structure your
work in a proper logical manner but it is impossible for you to immediately change all your habits and adopt all the new ideas and abstractions. You have probably seen a structure like

```
class someClassName
{
   //some methods and properties go here
}
```
and learnt that it is used in object oriented programming. It may be that in your project you are using those, you can build things with the use of an *interface* and *abstract*
keywords that do some extending but chances are that you actually create object instances rarely and prefer static method manipulation because this way of doing things seems more familiar.
 Well you are very close to object oriented programming, but not quite yet there. There is still a gap you need to cross and it is not easy to discover how to do that on your own.

## KISS principle
You are here because you want to write maintainable code. You want to be able to rapidly build new features. You are here because you want your code to be simple and easily scalable.

You want to *keep it simple, stupid*...

...and know enough to know that OOP is the way to go but even though you keep trying you still do not get all the benefits you thought you would get. Your project is
still affected by obscurity and complexity.

Well, in order to *keep it simple* we need to leave behind the *procedural world* and work only on objects (I will cover rare exceptions [later](#whengostaticsideeffects)) and follow some rules in a
disciplined way. Do not worry if some of the names in the table of contents make your head hurt - they might seem unclear but that is only because you are considering them against
the procedural way of thinking. I will soon show you that when you think in object oriented way this all actually makes sense.

*The larger the project gets the harder it is to keep it all simple* - that might be true in procedural world, where our minds need to keep track of complex procedures that make the project work. But in
OOP world you can limit the growth to a minimum thanks to the re-usability. There are techniques that help you design a convenient set of varieties that will not only be characteristic for your project
but are a cross-platform global standard. You learn about them once and done. All that remains is fun.

## *but the language allows for it!*
I have seen this argument a few times - the *language can handle it* as an excuse to keep an unfortunate design in. Trouble is it is not the language engine we should
be primarily concerned with. Computers are so fast today that an few extra milliseconds of runtime do not matter much. What is the real cost is the ability for the developers to
work with the code in an efficient manner. This is not an invitation into building a totally inefficient code that takes ages to execute, rather an encouragement to
make code readable if it will not cost much.

PHP allows for a lot. This language is so popular because it forgives so much. For example it is a *weakly typed* language which makes it easier to learn and operate
by junior developers for whom the idea of data types is not yet effortless. You can build your code in a non-strict way and the language allows for it but once
you gain more experience you realize that this has consequences as it can mean that your code will behave in an unpredictable way.

PHP allows for the code to work in a static manner even when we use classes, define interfaces to implement and create abstract classes to extend but it does not mean
that is a good practice as you are using the OOP features in a way in which they cannot spread their wings and show their true power. By sticking to static class usage
more likely you are introducing confusion in your team because everybody has to deal with the unexpected logic.

Avoid at all costs clever and/or hacky coding. Try not to show your programming skills by creating compressed constructs that use a logic custom crafted by your great
inventive intellect. Use logical patterns everyone is familiar with instead - that is what true wizards do! And always remember about the KISS principle!

> “Simplicity is the ultimate sophistication.”
> ―  Clare Booth Luce

# Object Oriented way of thinking
Since the time the first computer was built people had to create programs that would drive how it would function. The first programming languages were made to be directly
executed on the computers, the programmer would write commands understandable directly by the CPU but to an ordinary human being it was way too complex and alien. So smart
people came up with higher level languages that use syntax that mostly anyone can learn and understand. Programs written in high level languages are then interpreted or parsed and then compiled
to what a CPU can understand. This is where a new programmer usually starts their adventure - in the procedural high level language world.

Eventually to further the efficiency of the process on the human side some also very smart people came up with a revolutionary idea to create a way to describe enclosed logical entities into
the code and developed ways to manipulate such entities. Because that is how we, humans think - we live in a world of objects, abstract ideas that interact with each other. Anything you can
think of - be it a fork, a car, an animal, a factory, your manager, the planet, your lunch, even a certain idea in your head - all those are abstractions, entities that our brains are super fond of to use.
We can live surrounded by hundreds of those objects and we are perfectly fine. All those objects have some properties like a color or weight and all of them have some methods of what they can do like
move from one place to another or in the case of manager ask you to stay after work today. Once you become familiar with an object and what it does it just stays in your head easily.

In object oriented programming you create *blueprints* to describe an entity in the code and then you bring it to life by instantiating it. From now on this entity can interact with other entities to do
useful stuff. It is crucial to bring those entities to life by instantiating them because only then they can have some kind of internal state that can be manipulated. To our brains statelessness is like
filling a Tax Return form or doing any other sort of paperwork - it is soulless and procedural and we need to do thinking we are not naturally wired to do.

Any sort of procedural or static influence in your code (I will cover rare exceptions [later](#whengostaticsideeffects)) is like adding bureaucracy to the natural order of things.

You can create any sort of code with objects. Consider this:

```
//file Cow.php
class Cow
{
    private $is_hungry;

    public function __construct()
    {
        $this->is_hungry = true;
    }

    public function eat($food)
    {
        if ($food instanceof Food && $food->isConsumed() === false) {
           $food->setConsumed(true);
           $this->is_hungry = false;
        }
    }

    public function getMood()
    {
        if ($this->is_hungry === true) {
            return 'Mooooo! I am hungry and angry!'
        } else {
            return 'Moo! I am fine now.'
        }
    }
}

//file Grass.php
class Grass extends Food
{
}

//file Food.php
abstract class Food
{
    private $is_consumed;

    public function __construct()
    {
        $this->is_consumed = false;
    }

    public function setConsumed($value)
    {
        $this->is_consumed = $value;
    }

    public function isConsumed()
    {
        return $this->is_consumed;
    }
}

//file World.php
class World
{
    public function runAdventureOfLife()
    {
        $first_cow  = new Cow();
        $second_cow = new Cow();
        $food       = new Grass();

        $first_cow->eat($food);
        $second_cow->eat($food);

        echo 'First cow's mood: '.$first_cow->getMood().'\n';
        echo 'Second cow's mood: '.$second_cow->getMood();
    }
}
$world = new World;
$world->runAdventureOfLife();

//prints:
//First cow's mood: Moo! I am fine now.
//Second cow's mood: Mooooo! I am hungry and angry!
```

We have brought two cows to life (an immediately hungry ones) and made them eat the grass. One was the first to feast and ate the grass so the other one
did not have anything to eat. We can see that in the way they have expressed their feelings in the end.

It is just a funny example but it shows that we can create objects that hold their own state, can do things and can control other objects. Once you went through the code
is it easy to keep track of the relations between the objects, right? I bet it is, your brain loves this sort of things. There is no need for the
procedural paperwork. If we were to mix in any static methods then it would be like having to go through a line of bureaus and in each we would have to report what
is the current state of both of the cows and if the grass is already eaten or not before any cow will be let to eat.

We can add more functions to each object, add more objects making the World of Cows and Grass more functional. It all depends on what we are considering at the moment.

In the following sections I will describe how the real world works like. Because all the OOP principles you will read about also work in the real world. They
are meant to say *hey there, do not think computer code, think relations between objects*. Our minds when they think take all the rules below for granted, we just
need to point out that we need to stick to those rules also when designing our systems. Let's see how to define and build great object relations!

## Encapsulation.
The primary reason our minds like to work with objects is the fact that you do not have to declare every property of such an object and care about **ALL** it is capable of doing the exact
moment you think of it in a particular situation. You kind of wrap all those details behind one name and that is the layer our consciousness works in. When you take a pen into your hand you kind
of care only that it exists and that when you call ```swipeOverPaper()``` method for your hand that holds the pen, the pen's ```outputInk()``` method allows you to draw a line. You do not focus
about the laws of physics that drive the process, you do not care about how internally the pen is built, how much ink is left (until it is gone...) and of what chemical compounds the pen is made of.

The same approach is valid for the object oriented programming. The inner workings of an object are contained within that object and when we are using such object we care only about what it can
do for us and not the whole machinery inside of it. We *encapsulate* all the gears and wires and just use the object's exposed *interface*.

There are cases where you would want one object to work on the internals of the other like when a car mechanic needs to fix a car but if we can always design a car that does not break or is able
to fix itself once broken. If you can imagine it then you can code it.

Consider another example: a relation between a bank and it's client that has an account in such a bank. What if the client could directly modify the account balance without the use of the bank's
employees? One could set a million dollars into one's account and go on a shopping spree. The consequence would be probably a hyperinflation in the economy but it is not what matters for us now.
What matters is that the client should not be able to directly change any of the bank's properties such as the balances of the account's it holds. The client has to ask a bank employee to deposit
or withdraw the funds. The employee (acting as bank's *setter* and *getter* depending on the transfer direction) would first check the account balance, do validation if the client is who he/she
claims to be and optionally raise an alarm if it would detect a fraud. The bank has to be in a sole control of it's state and properties. The objects themselves should know better how to modify
their properties and state. It protects the integrity of the object as it's properties or state cannot be set to something invalid.

Every object needs to hide interactions and restrict access to it's inner workings. This is possible thanks to the *public*, *protected* and *private* keywords you put in front of the methods
and properties. Only methods that are meant to enable interaction with other objects should be *public*, everything else should be either *private*, or if we need [inheritance](#abstractclassesandinheritance)
features - *protected*.

Encapsulation also helps to limit relational dependencies between objects. Take a look at these two examples of ACL logic where an user wants to access a page and the acl needs to check if the user
has the necessary rights to do that. For the simplicity let us assume that the user already is instantiated and has the ```$id``` property already set. The general idea is that the ACL needs to fetch
some initial configuration to know how to proceed with the given resource (we have different types of resources ha!) and only then it is able to check if the user can access the resource.

```
//example without encapsulation

//file acl.php
class Acl
{
    public $config;

    public canAccess($resource_name, $user_id)
    {
        //code that tries to match in the database if the user can access the resource
        //the config property is used to do additional filtering in where clause
        //if match found returns true, otherwise false
    }
}

//file pageManager.php
class PageManager
{
    public function servePage($page_name, $user)
    {
        $acl = $this->configureAcl($page_name);
        if ($acl->can_access($page_name, $user->id)) {
            //render and return the page
        } else {
            return false;
        }
    }

    public function configureAcl($page_name)
    {
        $acl = new Acl();
        $acl->config = $this->getPageConfig($page_name);
        return $acl;
    }

    public function getPageConfig($page_name)
    {
        //the config is being fetched from the database
    }
}

//file user.php
class User
{
    public $id;
}

$page_manager = new PageManager();
$page = page_manager->servePage('pageAboutKittens', $user);
if ($page !== false) {
    //echo the page to the browser
} else {
    //return error code 403 forbidden
}
```

```
//example with encapsulation

//file acl.php
class Acl
{
    $private $config;

    public canAccess($resource_name, $user_id)
    {
        $this->config = $this->getResourceConfig($resource_name);

        //code that tries to match in the database if the user can access the resource
        //the config property is used to do additional filtering in where clause
        //if match found returns true, otherwise false
    }

    private function getResourceConfig($resource_name)
    {
        //the config is being fetched from the database
    }
}

//file pageManager.php
class PageManager
{
    public function servePage($page_name, $user)
    {
        $acl = new Acl();
        if ($acl->can_access($page_name, $user->getId())) {
            //render and return the page
        } else {
            return false;
        }
    }
}

//file user.php
class User
{
    private $id;

    public function getId()
    {
        return $this->id;
    }
}

$page_manager = new PageManager();
$page = page_manager->servePage('pageAboutKittens', $user);
if ($page !== false) {
    //echo the page to the browser
} else {
    //return error code 403 forbidden
}
```

Both cases are designed in a rough way and could use a lot of improving but anyway there is a significant advantage the second example has over the first one -
the ```Page``` object does not get to do the job of configuring the ```Acl```. ```Acl``` configures itself.

It might feel convenient to go the first way if your focus is aimed at having the process of serving the page robust because you think that a strong page manager
should be in control of everything. But what will happen when you will need more such managing objects - for example one that serves files or you will make the new
API and have it also configure the ACL it is going to use. Suddenly you have multiple entities that control the property of the ACL. Now let's say there comes a new
security requirement from one of your business clients where all attempts to configure the ACL need to be logged. In order to achieve this all those multiple entities
will have to have the code that manipulates the ACL's config property changed and believe me when I say that for the most of cases only one or two will get changed and
as more time passes and more developers work in this area the more the implementations will drift away from each other making the code base larger, more confusing and complex.

The ACL should be able to handle it's inner workings without any additional help. It can accept parameters it will understand and change the way it is working but it
has to do the work on it's own.

We also can encounter problems with directly fetching the user's id - perhaps we would want the ```User``` object to check in the future in what environment it is in before
serving the id, for example in order to do some testing in development environment we could add:

```
//file user.php
class User
{
    private $id;

    public function getId()
    {
        if (IS_DEVELOPMENT) { //IS_DEVELOPMENT is a system global set when the application starts by some core code
            //override with admin id
        } else {
            return $this->id;
        }
    }
}
```

In the first example it is impossible to do. We access the id property directly. The worst part is that at the time of writing the code we had no way of
knowing that we will need such a feature. That is why it is important to stick to good coding principles at all times - you never know when they will save the day.

So to sum up - avoid direct assignments and accessing of other object's internal properties. Use only the object's exposed interface.

## Polymorphism.
Do you have a driving licence? If so then you can drive any car of any make. All cars can be controlled in the same way - you have the steering wheel, some pedals
and a way to control the gears. In other words all cars share the same interface.

The car can run on hydrogen, gasoline or be entirely electric. The suspension can be based on springs or hydropneumatic. The car can be made to be fast or to be able
to carry extra load. The number of variations is limitless but as long as they have the same interface - they all can be operated in the same way by the same person.

If you had to take your car to the mechanic you can totally borrow your partner's car to go to work - in other words you can replace the objects that share the same
interface without any issues.

Consider the following scenario. A web shop administrator needs to view the details of a person - the first time it will be just a member (client) of the web shop and then the
admin will need to view the details of a certain employee. Depending on the case a proper object will be instantiated by the application - either Member or Employee in an
appropriate area of the system.

```
//no polymorphism

//file Member.php
class Member
{
    public function getMemberAddress()
    {
        //fetches member home address from the db
    }

    public function getFirstName()
    {
        //fetches member first name from the db
    }

    public function getLastName()
    {
        //fetches member last name from the db
    }

    public function getContactInformation()
    {
        //fetches telephone number and email address from the db
    }
}

//file Employee.php
class Employee
{
    public function getContactDetails()
    {
        //fetches employee home address, telephone number and email address from the db
    }

    public function getCredentials()
    {
        //fetches employee name and last name from the db
    }
}

//file RenderDetails.php
class RenderDetails
{
    public function renderView($person)
    {
        if ($person instanceof Member) {
            $contact     = $person->getMemberAddress().'\n'.$person->getContactInformation();
            $credentials = $person->getFirstName().' '.$person->getLastName();
        } elseif ($person instanceof Employee) {
            $contact     = $person->getContactDetails();
            $credentials = $person->getCredentials();
        } else {
            //return error
        }

        //use a template file to render the details with the use of $contact and $credentials variables
    }
}

//case view member in member administration area
$detailsRenderer = new RenderDetails();
echo $detailsRenderer->renderView($member);

//case view employee in employee administration area
$detailsRenderer = new RenderDetails();
echo $detailsRenderer->renderView($employee);
```

```
//with polymorphism

//file Person.php
interface iPerson
{
    public function getContact()

    public function getCredentials()
}

common address, age and other personal data, contact information

//file Member.php
class Member implements iPerson
{
    public function getContact()
    {
        //fetches member home address, telephone number and email address from the db
    }

    public function getCredentials()
    {
        //fetches member name and last name from the db
    }
}

//file Employee.php
class Employee implements iPerson
{
    public function getContact()
    {
        //fetches employee home address, telephone number and email address from the db
    }

    public function getCredentials()
    {
        //fetches employee name and last name from the db
    }
}

//file RenderDetails.php
class RenderDetails
{
    public function renderView(iPerson $person) //type hinting makes sure the object will have the methods called below
    {
        $contact     = $person->getContactDetails();
        $credentials = $person->getCredentials();

        //use a template file to render the details with the use of $contact and $credentials variables
    }
}

//case view member in member administration area
$detailsRenderer = new RenderDetails();
echo $detailsRenderer->renderView($member);

//case view employee in employee administration area
$detailsRenderer = new RenderDetails();
echo $detailsRenderer->renderView($employee);
```

In the first case if there will be ever any more variations of a person's role you will also need to include how to interact
with them in the RenderDetails and whatever area is using it. In the second example the consuming code only cares about the interface and you can add as many new roles
as you want and not worry. The code is much more scalable.

When and how to use polymorphism? In the above, first no-polymorphism example if the Member class was designed well before the Employee class then whomever was designing
Member class would probably not be able to foresee that the existence of an interface would be beneficial in the future and chose not to overengineer by creating an interface file.
On the other hand the developer that designed the Employee class could not know the code base so well to be aware of the existence of the Member class.
If none of the two developers were able to find any reason to create an interface then the third one that was tasked with building or extending the RenderDetails class should
have done a little refactoring in order to build a common interface for both the Member and the Employee. That is because obviously - that developer had to see that there
is a very similar pattern taking place. Refactoring might be costly, especially if the Member and Employee classes are already being used widely in the system... but then
again it is just because someone had failed to make a common interface for them in the past. And the technical debt just kept growing.

If you ever work with a code and there are two or more objects that are being used in a very similar way - then make sure to consider specifying an interface and then code
for that interface.

### Polymorphism in static world.
Some sort of polymorphism behaviour can be done in the static world the help of [late static bindings](http://php.net/lsb) in PHP.
But is merely like trying to reuse some of the OOP advantages in the procedural world and it can only lead to making a *hacky* code.

## Abstract classes and inheritance.
In the Real World we use the word *inheritance* to describe the process of when a child gets something from their parents. It can relate to inheriting a house, or maybe
somebody inherited a pointy nose. We can even use this word to describe how each generation is able to create new technical advancements based on the knowledge and
experience of the past generations.

But let us get back to the pointy nose. Thanks to Charles Darwin we know about an incredible force that can mold life forms called *evolution*. If we dig far enough into
the past we find out that all species share similar characteristics to some degrees. Plants and animals are built from cells that contain similar ogranelles. A little closer
in the ancestral tree of life in the animal kingdom one can highlight *Chordates* phylum and all species contained in it have some sort of spine. The closer we are in the
classification to the concrete species the more sophisticated and complete the list of a given life form features will become. If we were to biologically
classify for example humans, dogs and dolphins we could write it like that:

```
for humans:
HomoSapiens extends HomoGenus extends HominidsFamily extends PrimatesOrder
extends MammalsClass extends ChordatesPhylum extends AnimalsKingdom extends Life

for dogs:
CanisLupus extends CanisGenus extends CanidaeFamily extends CarnivoraOrder
extends MammalsClass extends ChordatesPhylum extends AnimalsKingdom extends Life

for dolphins:
TursiopsTruncatus extends TursiopsGenus extends DelphinidaeFamily extends CetaceaOrder
extends MammalsClass extends ChordatesPhylum extends AnimalsKingdom extends Life
```

Clearly some classification levels are the same so let's throw them away. We deal only with three species all being mammals so let us just throw all features and functions or Life,
AnimalsKingdom, ChordatesPhylum into MammalsClass.

```
for humans:
HomoSapiens extends HomoGenus extends HominidsFamily extends PrimatesOrder extends MammalsClass

for dogs:
CanisLupus extends CanisGenus extends CanidaeFamily extends CarnivoraOrder extends MammalsClass

for dolphins:
TursiopsTruncatus extends TursiopsGenus extends DelphinidaeFamily extends CetaceaOrder extends MammalsClass
```

This is better but in order to tell the differences between the species we can just focus on the Order classification level and remove the details that come with the Family and Genus
levels:

```
for humans:
HomoSapiens extends PrimatesOrder extends MammalsClass

for dogs:
CanisLupus extends CarnivoraOrder extends MammalsClass

for dolphins:
TursiopsTruncatus extends CetaceaOrder extends MammalsClass
```

Now because latin is a dead language and this is about writing code let's do a final modification:

```
//Abstract classes
//file Mammals.php
abstract class Mammals
{
    //contains all methods and properties of living matter, animal kingdom cell structure,
    //chordates spine and bone structure and finally mammal's neocortex and ability to produce milk.
}

//file Primates.php
abstract class Primates extends Mammals
{
    //covers more advanced brain capabilities, high reliance on vision and precise fingers
}

//file Canines.php
abstract class Canines extends Mammals
{
    //covers teeth adapted for cracking bones and slicing flesh, legs created for quick running
}

//file Whales.php
abstract class Whales extends Mammals
{
    //covers having fins for locomotion, slick body adapted for water environment
}

//Concrete classes
//file Human.php
class Human extends Primates
{
    //covers specific human features - upright posture, capability of abstract thinking, self awareness,
    //high intelligence, very precise fingers
}

//file Dog.php
class Dog extends Canines
{
    //covers type of fur, human friendly behaviour, ability to learn tricks, reliance on smell senses
}

//file Dolphin.php
class Dolphin extends Whales
{
    //covers the skin color, long nose, reliance on echolocation sense
}
```

The best thing about being able to use abstract classes is that you can put common concepts, properties and methods in them and only focus
on the very specialized features in the concrete classes.

Abstract classes cannot be instantiated - they are... well abstract. Unable to exist on their own. They only describe the concept, the inner workings. So for
example you cannot instantiate Mammals because it describes the general architecture of a life form but otherwise is incomplete to live on it's own.

Consider the example below:
```
//no inheritance
//file Users.php
class Users
{
    public function getRows()
    {
        return $this->getRowsFiltered();
    }

    public function findUsers($name)
    {
        return $this->getRowsFiltered(['name' => $name])
    }

    private function getRowsFiltered($filters = null)
    {
        //retrieves rows based on the filters
    }
}

//file Products.php
class Products
{
    public function getRows()
    {
        return $this->getRowsFiltered();
    }

    public function findProductsByPrice($price)
    {
        return $this->getRowsFiltered(['price' => $price])
    }

    private function getRowsFiltered($filters = null)
    {
        //retrieves rows based on the filters
    }
}
```

```
//with inheritance
abstract class AbstractTable
{
    public function getRows()
    {
        return $this->getRowsFiltered();
    }

    protected function getRowsFiltered($filters = null)
    {
        //retrieves rows based on the name of the calling class and applies filters
    }
}

class Users extends AbstractTable
{
    public function findUsers($name)
    {
        return $this->getRowsFiltered(['name' => $name])
    }
}

class Products extends AbstractTable
{
    public function findProductsByPrice($price)
    {
        return $this->getRowsFiltered(['price' => $price])
    }
}
```

In the first example each concrete class needs to be able to fully define the way it works. In the second one the two concrete classes simply
inherit the inner mechanics from the abstract class. This not only allows for smaller and cleaner concrete classes but also allows you to prevent
duplication. If one functionality is defined in just one place then it is much easier to change it as you do not have to edit it in multiple places
at the time. Even worse - somebody in the first example might have changed the way the ```getRowsFiltered()``` method works in one class and forgot
to do that that in the other and now we have two different conventions in the code. The more differences like that the more coherence in the general logic is
lost and the harder it gets to understand it. Eventually there will be different kinds of logic in the code doing pretty much the same thing. We do not want that.

### Composition and inheritance.
It is easy to get lost with inheritance and to rely on it too much. It lets you build very powerful objects that can do many things but making objects that are
a dumping ground for every conceivable logic only means that you will sooner or later get lost in their many competencies. Eventually you will begin to write
very similar methods or methods that do the same things because you will not be able to encompass it all. To prevent this take a look at the
[single responsibility principle](#singleresponsibility). In short rather than for example defining the functionality of all body parts you compose
the life form using one *wrapper* object and then you would add smaller ones to it like *Heart*, *Limb*, *Brain*. The wrapper object would still be in
control of the smaller ones but it would not care about how internally each smaller object works thus one can move vast amounts of functionality into
smaller logical, specialized chunks.

Below are two problems that might occur if we abuse the use of inheritance.

#### Over-inheritance.
In the example about the human, dog and the dolphin I did cut the initial classification levels because we did not need such a deep and detailed taxonomy.
This is all relative to the case but do not inflate the abstract classes stack just for the sake of inflating it because you think it might be useful. Always
keep the narrowest logical structure that explicitly covers the differences in the concepts you need otherwise you risk introducing confusion as to why you
did so much dividing.

#### Abstract monoliths.
This is the other direction. Do not stash a humongous amounts of functionality into one abstract class. It might sometimes make sense to arm the concrete classes
with a wide arsenal of methods but once you start inflating an abstract class then eventually it will be difficult to say what kind of an abstraction it contains. This
often leads to a situation where the control is being lost and virtually everything even only remotely related to the initial logic is being dumped into one class. Or worse also
copy-pasted into a similar abstract monoliths elsewhere.

##### Refactoring of abstract monoliths.
Because abstract monoliths usually get built over a long period of time they will contain many different kinds of logic and many overrides inside their bodies. Because of those overrides
it might be very hard to refactor them. Even if you manage to make some sense of what each method is doing you still have to be aware of the overrides that people put inside the methods
to solve one isolated issue in the shortest possible (and messy) way. So once you split the methods into smaller objects you might find shortly afterwards that lots of customized behaviour
stopped working and you will be forced to revert all your work back because the refactoring will be taking too much time already.
What can you do in such case? Nothing much with the monolith I guess. If you have more of them then perhaps it is time to try to think about how much development time gets wasted by trying to maintain them.
If it is a significant portion then it might be a good argument to start thinking about moving to a new platform which will be free of past mistakes.

The move to a new platform is always inevitable if only because of the constantly changing technologies and if properly built and maintained can quickly take over the responsibilities of the old one. Bear in
mind that technologies evolve and get improved over time so it is very possible that the move can be less costly than you would expect and it would be also a great opportunity to remove ancient
functionality that no-one needs anymore.

### Inheritance and encapsulation.
> “Because inheritance exposes a subclass to details of its parent's implementation, it's often said that "inheritance breaks encapsulation".”
>  — Gang of Four, Design Patterns

In general you should avoid overriding the methods of the parent's class. Because you are introducing a difference in the convention used by that abstract class.
If you override a behaviour that is meant to be common across the objects that inherit it then you are creating something new. In a case like that you might consider
adding another level of abstraction and move the behaviour needed to be changed there. Just be careful not to over-inherit.

### Abstract methods.
Abstract methods can be used to further define some characteristic of an abstract class without defining the implementation of such characteristic.
Let's get back to the biological classification example. All life forms must be able to reproduce so we can define something like that:

```
//file LifeForm.php
abstract class LifeForm
{
    abstract private function reproduce()
}

//file Flower.php
class Flower extends LifeForm
{
    private function reproduce()
    {
        //sends out pollen and/or collects pollen to kick off the creation of seed
    }
}

//file Fish.php
class Fish extends LifeForm
{
    private function reproduce()
    {
        //lays eggs to be impregnated/impregnates the laid eggs
    }
}
```
We know we need reproduction for life to thrive but since different forms of life reproduce in different ways we cannot define any method in the abstract
class. We have to leave the implementation to the concrete classes and they **must** implement it in some way.

### The idea of interfaces (polymorphism) can be sometimes mixed with abstract classes (inheritance).
That is because these two are about some very similar concepts. Both are used to describe ways in which objects that use them work.
However while the interfaces define how the object should interact with other objects the abstract class is used to describe how the internals of the object should work.
In other words the abstract class is a general template of what an object is and the interface is about what the object can do for other objects.

To better spot where the responsibilities should go remember about [encapsulation](#encapsulation) - basically an interface should never care about the inner
machinery of an object. It describes that you need a driving wheel, the pedals and the gear controller but it does not care how the car work under the hood.
It is the job of an abstract class to describe what is happening under the hood - the general concept of how the engine works, the breaks and the transmission
so that concrete car implementations do not have to repeat the same ideas all over again.

Interfaces should never be used to drive how a object processes a certain task. An abstract class should never contain method
stubs for the sole purpose of having them overridden (although nothing stops you from having an abstract class implement an interface) by child classes.
Any deviations will only cause consternation and will make the code hard to [understand](#butthelanguageallowsforit).

### When to use?
When you have two or more objects that have a very similar characteristics - you can move the common functionality to the abstract class. Or if are designing something new
and know that there will be many similar objects in the current project you are working on - create a common abstract class for them in the very beginning, but beware
of [over-engineering](#overengineering).

## Delegation.
Delegation happens when you need a middleman that will enable cooperation between the client object and the providing object. No-one likes middlemen as they
raise the price of service but the client might not possess such a specialized knowledge to know how to go around the middleman.

For example let's say you are feeling ill and need to see a doctor. So you go to a general practitioner that can make an initial diagnosis and direct you to
a specialist that will be able to help you if it is out of GP's abilities. Basically the responsibility of curing you got delegated to somebody else.

The greatest advantage of this arrangement is that not everyone has to have the knowledge of a GP in order to get cured. You just go to a doctor and he provides
a solution or delegates it to somebody who knows better.

One example of a use in the OOP would be when a controller objects need a templating engine to build some kind of a view for it. The view object depending on
the context might simply pass this request to a specific decorator or a different view helper.

### Dynamic delegation.
In general I would highly discourage the use of any dynamic class/method calling. The reason is that such relations cannot be mapped and indexed by an IDE which
means that any future refactoring will be very painful. You could use ```@used-by``` or ```@see``` tags in the docblocks to highlight in a particular method or
class that it can be potentially called dynamically by some other parts of the code base but this is a weak and ugly solution.
If you see a lot of those ```call_user_func()``` in the code you are working with then perhaps you have a developer in your team that also does coding in
C, C# etc. Dynamic delegation is useful there for keeping the application running when it needs to respond to events but PHP works in a different way. Most of
the time there is a request, the server-side code parses it, deals with it and returns a response. In an environment like that it is very hard to be in a
situation where you will not be able to know what class or method will need to be called before runtime.

In some rare cases however you might indeed have no choice but to use dynamic delegation. For example when working with libraries like AMQP/RabbitMQ where you
create a queueing system for large, resource consuming tasks or when developing an API using SoapClient. These technologies use dynamic delegation because the
functionality requested by the client will only be known when the script is either already running (in case of the queue) or the library is just really old
(SoapClient).

If you have no choice then make sure that you at least document the uses and keep the documentation up to date. It might save you from a very heavy headache.
But if you have a choice and considering options - if you are working within your own platform and have the luxury of being able to properly parse any
requests hitting your server and API - then just don't use any dynamic calling. It is simply unmaintainable. It might be convenient for you now but it might
be a hidden future cost!

Remember that high level languages and OOP were not invented to make it easier for the machine but to make it easier for the human. Most developers use some
sort of an IDE to make it all even simpler and faster - make sure you do not make it harder to use them.

## When go static, side effects.
There are some cases where the use of static methods would not hurt anyone. It is when a given method does not produce any *side effects*. What
it means that if the class is simply going to return the result of a calculation between two variables then by all means - make this work in a static manner.
It does not matter really much. But if the class needs to change contents of different classes/objects, fetch additional data, it outputs any headers or simply
can throw any exceptions then don't go static. If your method has the capabilities of changing the application's state in any way then it should also be able to
hold a state (it's object that is) if only for the sake of being able to log it when things go boom.

Okay, there is also one more good reason to go static. If you are working with an old code base and if not going static would mean introducing new conventions
and confusion - then for the sake of everybody else do things the old way. Unless refactoring of the convention is not out of question. However if it is a large
project then chances are it is simply financially unfeasible to do.

However remember that static should be avoided if possible. In my personal opinion there is simply no good reason to go static when you do not have to other
than just being lazy.

### Design patterns.
Some design patterns that were invented a long, long time ago use static classes to do things. That is okay since these are some well thought behaviors and
conventions.

## Summary: OOP
Object Oriented Programming is about using data types called objects that act as wrappers for a given type of functionality. The most useful features of object
oriented code is that it is much more easier for human mind to remember object based relations over the procedural scripts and that object oriented code is much
more re-useable which might lead to a smaller and more cohesive code base.

A good OOP code contains a mix of the following techniques:
+ [Encapsulation](#encapsulation) - hiding of the inner workings of an object from the code (other objects) that is using it. This helps the developer to focus on the current job without having
to know how the object being used as dependency exactly works which can ease up the work immensely.
+ [Polymorphism](#polymorphism) - ability to use different concrete objects that use the same interface. This lets the objects that require the dependencies to work to be smaller
as they do not have to *know* how to use the many different interfaces.
+ [Inheritance](#abstractclassesandinheritance) - ability to contain common functionality into an abstraction. The abstractions can be inherited by concrete objects and thus they do not have
to define everything themselves, only their very specialized features. Enables inner functionality segregation.
+ [Delegation](#delegation) - the consuming class does not have to know every single dependency and thier interfaces for each possible task. It can use more general 'middleman' objects that wrap some
functionality inside them and know more specialized actors that can get a certain job done. This allows for a better separation of concerns since the consuming
class does not have to know *everything* about the code base it is in.

# SOLID
What can be said about SOLID at the very beginning is that the rules might make no sense at first. They require you to spend extra time while building code because not
only you have to *get the job done* - you also have to make it compliant with some rule set. However if you follow this rule set it will prevent you from introducing a *technical debt* into the code base.
What is a technical debt? Well most of the time it is adding new, unconventional logic into the project. The more times you do that the harder it will be
to keep track of how the system is working. Technical debt is also when instead of refactoring the code in light of the new requirements you add new logic
(even if conventional) by overriding the current functionality. As a result there will be two or more ideas of how to do a certain thing and it has a habit of quickly getting worse.
The SOLID rules help prevent introducing of the technical debt because of the way you build the system using SOLID - it makes it easier to understand and keeps the
code base as small as possible. Discipline is required as in general it makes writing new code a little bit harder too.
The more experienced you will become the more you will look at the SOLID rules as not unnecessary fuss but a salvation. The extra time you will have to spend doing
any piece of code with respect to the SOLID rules will be earned back with a premium the next time somebody has to work in this area. And the next time. And the next time.
And the next time. And the next time. And the next time...

It is not always so straightforward in determining where lies the correct balance - because you can over do in making sure your code is beautiful just as well.
But remember not to use that argument to justify writing bad code - if you think you are committing a programming sin - then probably you are.

For one-off projects it is best to just do whatever it takes to make them work. For projects that will require a long-term maintenance - the adaptation of SOLID rule set is
strongly advised.

The SOLID rules relate to each other and together form harmony. They are also compatible with [Encapsulation](#encapsulation), [Polymorphism](#polymorphism),
[Inheritance](#abstractclassesandinheritance) and [Delegation](#delegation) features of OOP and aid in a proper utilisation of those features.

## Single responsibility
This is one of the most important things to keep in mind when building good code. If you think it can be hard for you to keep in mind every SOLID rule when you build
code then simply just stick with Single Responsibility Principle and you will be fine - the rest will come naturally later.

I have mentioned that stashing huge amounts of functionality into a single class is not the best idea already [here](#abstractmonoliths), when talking about abstract
monoliths. The more functionality the class receives the harder it gets to keep track of what it can actually do. Not even the senior developers will be able to remember
all of it and they will end up writing entire features from scratch because the logic of the old solutions will get simply lost in the many thousands of lines of a monster
class or classes.

So we want smaller, specialized objects with defined narrow responsibilities interacting with each other rather than a few huge objects executing their logic one by one.
'But how narrow a *narrow* is?' - one might ask. There is no one defined standard of defining of how deep one needs to go dividing responsibilities to succeed in having a
maintainable system. There are only general guidelines and a heavy reliance on common sense. Consider the following:
+ one class should only be a couple of hundreds lines long at maximum. If it grows beyond let's say 400 lines then it is most likely being overinflated with responsibilities.
Use composition, delegation and inheritance to limit the size.
+ as Robert Cecil Martin, co-author of *The Manifesto for Agile Software Development* says: *A class should have only one reason to change*. What this means is that when
some functions of the system have to change you should seek a different class to implement those changes for each type of change. For example putting into one controller the logic of rendering a view
and also setting up ACL module that drives access to that view is wrong. The controller should completely delegate that task to specialized objects. The controller's
responsibility should be only limited to in fact - delegating tasks. So next time you will want to add a method to a class look at the other methods and what they do. Look at
in what context this class is being used elsewhere and check how similar objects are being used. If your functionality does not fit into the general idea then it is not the right
place to put it in.
+ more help can be found in [Interface Segregation](#interfacesegregation) section below. By defining and sticking to an interface you can lower the load of having to think
whether an object is getting a responsibility creep. You only need to make sure you are working *within* said interface.
+ some basic examples of objects with single responsibility by category:
    + managers/controllers - should only process a single parsed type of request - where the types are in general very similar. Does not do any business logic - it only calls
    in succession more specialized objects and passes control between them,
    + models - should be a representation of an entity - a document, a row in the database, a table in the database, a user etc. Every model can be also composed of smaller ones.
    Models should be very selfish and care only about themselves - they should provide an interface for modifying their state or providing some specialized service,
    + factories/producers/builders - it is very useful to delegate the responsibility of creating other objects like models to creational objects. They help in decoupling of
    whatever is being created from the clients that need them,
    + adapters/converters - the sole purpose of them is to facilitate cooperation between two different systems.
    + renderers/decorators - should only contain logic that renders a view to be outputted to a browser or to a document. Should only accept simple parameters and should never
    have to know how to interact with objects other than those that create the view stack.
    + response/request handlers - handle intercepting requests, parsing them and giving the request data to the controllers. When controllers end their job they should give the
    response data to the response handlers.

In the real world if you were to have a workshop you would have many different tools that can be used to help you perform one and only one type of handiwork. There of course
exist some omni-tools but very often they are large and not very good for specific activities.

> "If something is for everything then it is for nothing".

Single responsibility principle can be used with the term **separation of concerns** interchangeably.

### Method responsibilities.
Similar rules apply to the methods inside a class. Only that they are even narrower. Do not build mega methods that span more than 50 lines of code that do everything. Split
a process into smaller, logical chunks, especially if you can see some similar blocks of code in two or more mega-methods.

### Tight couplings, loose couplings.
Any well designed class should have a simple interface and be reusable when different parts of the system require services that this class provides. That way your
code base can remain relatively small. In order to get something done you should only be able to call an object via a simple interface and optionally receive
a finalized response. The process of building such a response should be encapsulated and invisible to the caller. That way of doing things is called loose coupling.

When the creation of such a response is being spread among many different classes that bounce the data between them in order to provide the response - it is
called tight coupling. The more complex the interacting process, the more design of one class depends on the design of the other, the harder it is to implement
that process elsewhere - thus it often leads to the creation of a monstrosity that is either a one-time contraption or is very costly to maintain and re-use.

Consider the following example. Let's say we have a website with many different areas like News, Blog, Store. Each such area has it's own controller that is able to
take in a parsed request and call specialized objects that contain the business logic to do some tasks like updating records or rendering a view based on templates.
Some actions are to be accessible only to the website's subscribers and some only to the moderators. So for each request we need to check who the current user is and
if s/he should be permitted access to a specific resource.
It might make sense to be able to define the permissions inside the controller - be it inside the class, a separate .ini file or in some page configuration area in the
database, because it concerns permissions for this given page. Such configuration would then get passed into another object that would check if this configuration
is not in conflict with some more generic ACL sub-system before the controller would be finally able to grant a permission for the user to access a given resource.
```
//file SomePageController.php
class SomePageController extends PageController
{
    private function getConfiguration()
    {
        //fetch page configuration
    }

    //checks if action can be performed
    private function canPerformAction($actionName, $currentUser, $resourceName)
    {
        $permissionChecker = new PermissionChecker();
        $availablePermissions = $this->getConfiguration()['availablePermissions'];
        return $permissionChecker->canAccess($this, $currentUser, $resourceName, $availablePermissions)
    }

    public function uploadDocument(Document $document)
    {
        //user got injected in the constructor into $user property, so we provide it like that

        if ($this->canPerformAction('upload', $this->user, $document->getType()) === true) {
            //send the document to the database
        } else {
            //return error message
        }
    }
}

//file PermissionChecker
class PermissionChecker
{
    public function canAccess(PageController $controller, $currentUser, $resourceName, $availableActions)
    {
        //check the type of the controller - if ACL allows user role to access it, if not return false
        //check if the resource name is present in available actions configuration, if not return false
        //check if the user has any association with the resource requested (like being an author of a document)
        //etc more checks that you can imagine
        return true;
    }
}
```

The trouble with the example above is that the process of getting the *availableActions* list and evaluating against then is
being done by basically two objects. The controller instead of just controlling is getting some extra jobs. The
*$availablePermissions* parameter needs to be formatted in a specific way for the *PermissionChecker* to be able to work with it.

So what happens if we want to add such permission checking process to different pages? More controllers will have to have their inner
design tightly coupled with the *PermissionChecker* and will have to contain and execute more or less the same logic.

What if a few pages have this functionality already and we want to refactor the solution or simply fix a bug? Instead of doing it
only in one place we will have to evaluate every tight coupling made. A recipe for a very slow development process as it is hard to
get your head around which class is the *core* actor for the overall process when responsibilities are spread across
two objects and there is no encapsulation. It might mean that in the future somebody will *expand* the functionality by adding it
to a one particular controller rather than adding it to the permission checker.

Let's make the controller's life a little easier and remove the need to fetch and format the *$availableActions* and have the
*PermissionChecker* do it instead:
```
//file SomePageController.php
class SomePageController extends PageController
{
    public function uploadDocument(Document $document)
    {
        $permissionChecker = new PermissionChecker($this);

        //user got injected in the constructor into $user property, so we provide it like that
        if ($permissionChecker->canAccess('upload', $this->user, $document->getType()) === true) {
            //send the document to the database
        } else {
            //return error message
        }
    }
}

//file PermissionChecker
class PermissionChecker
{
    private $controller;

    public function __construct(PageController $controller)
    {
        $this->controller = $controller;
    }

    public function canAccess($actionName, $currentUser, $resourceName)
    {
        $availablePermissions = $this->getResourceConfiguration($resourceName);
        //check the type of the controller - if ACL allows user role to access it, if not return false
        //check if the resource name is present in available actions configuration, if not return false
        //check if the user has any association with the resource requested (like being an author of a document)
        //etc more checks that you can imagine
        return true;
    }

    private function getResourceConfiguration($resourceName)
    {
        //fetch resource configuration
    }
}
```
We have lost the ability to define the available actions for a given page that the controller is driving and instead made the
*PermissionChecker* fetch the configuration itself. Let's say we have moved the configuration UI from page administration to
ACL administration where I believe it would fit in much better anyway.

The move made the controller not concerned with one parameter so the coupling level has been lowered to a much more manageable level. Basically
right now the controller only cares about the *$actionName* parameter and all other parameters are just being passed over and could have been
[injected](#dependencyinjection) as the *PageController $controller* was in the *PermissionChecker*'s constructor.

Even better if we could move the ```$permissionChecker = new PermissionChecker($this);``` into some kind of overall initialization logic for the
controller's parent and make it part of the controller's state.

#### Dependency Injection
Check the second example in the section about [tight and loose couplings](#tightcouplingsloosecouplings). I made a little trick in the ```PermissionChecker```
class:

```
    private $controller;

    public function __construct(PageController $controller)
    {
        $this->controller = $controller;
    }
```

This is called Dependency Injection and from now on the object can use the controller in whatever way it wants. The main advantage of doing things like
that is that a given object does not have to care about how, where and in what state to get the dependencies that are necessary to perform the main task
of the object.

You can pass the dependency after the initialization via a method but it is just safer to declare all dependencies at once if possible. If you do it after
initialization then there is a risk that some method that needs the dependency will be called before the method that receives the dependency.

Please note that that in our example we are injecting the base object of *PageController* class and not the *SomePageController* sub-type - this
enables us to inject any page controller into *PermissionChecker* and not just one. Or in other words any page can use the same *PermissionChecker*. It
is another loose coupling that allows the code to be re-used.

In the examples throughout this document I did not (mostly) use dependency injection so the code is easier to read for somebody not accustomed to seeing
injection in action.

#### Spaghetti code
You might have came across a term *spaghetti code*. You can kind of imagine a tightly coupled code to be a bowl of spaghetti where code flows in manner that is
very complex and impossible to track. Spaghetti code attacks when many developers work on the same area of the system and each one implements his/her own logic
rather then trying to understand the general concept of the area they are trying to modify first.

Remember [not to invent](#extradonotreinventthewheel) things when you do not have to. Always try the smarter way first of re-using what you already have.

## Open/Closed principle
This rule means that an interface concept should be *open* for modification only during an initial planning and design process. Once the interface gets implemented
by any class that makes it's way to production the interface should be *closed* against any further modification. And there is a good reason for it.

If object FOO depends on object BAR it means the FOO will be making the use of the BAR's interface. If we change the interface of BAR then we will have to change
the FOO as well. Even worse when more objects use BAR, we will have to change them too! In an old system this can be very risky.

There is however nothing against extending BAR with new functionality or even changing the way the interface is implemented - as long as it does not change anything
from the FOO's perspective. BAR is *open* for extending.

## Liskov substitution
While discussing inheritance I have mentioned that [you should not override parent's methods](#inheritanceandencapsulation). Liskov substitution is about the same
thing. It says that the parent class should be able to be replaced by it's child class without any problems and without causing bugs.
If you are extending a class then make sure the extending functionality does not break the convention and the way the functionality should be used in.
Look at the example below:
```
//file RenderListHelper.php
class RenderListHelper
{
    public function renderList($listItems)
    {
        $listView = '<ul>';
        foreach ($listItems as $listItem) {
            $listView .= '<li>'.$listItem.'</li>';
        }
        $listView .= '</ul>';

        return $listView;
    }
}

//file ChristmasRenderListHelper.php
class ChristmasRenderListHelper extends RenderListHelper
{
    public function renderList($listItems)
    {
        $listView = parent::renderList($listItems);
        $listView = str_replace('<li>', '<li><span class="christmasColors">', $listView);
        $listView = str_replace('</li>', '</span></li>', $listView);

        return $listView;
    }
}

//file PageController.php
class PageController
{
    private $listHelper;

    public function __construct(RenderListHelper $listHelper)
    {
        $this->listHelper = $listHelper;
    }

    public function getProductList()
    {
        //how we receive the products list is not important in our example so lets just assume we have them in $products
        return $this->listHelper->renderList($products);
    }
}
```
The way the *ChristmasRenderListHelper* extends *RenderListHelper* is safe and does not violate the Liskov substitution rule. We can use any of them at
any time and the code will work when we call *getProductList()*.

If the extending class will override the behaviour of the parent's class - for example rendering a table instead of a list - then this rule will be
violated. The more such violations the more useless and confusing the fact that we are extending something will be.

## Interface segregation
Interfaces should be small and compact. They should describe an activity and what a class that implements them can do. But most importantly the interfaces
should be aimed at providing the right functionality to the objects that need it.

In other words do not design an interface to describe the objects that will implement it but rather design an interface based on the objects that will be
calling it.
Remember that in PHP you can have an object implement as many interfaces as you need, although remember about the [Single Responsibility Principle!](#singleresponsibility).

A system with a set of well defined tiny interfaces and abstract classes is generally self-hinting and self-explanatory everywhere you look.

### Frameworks come with some segregation already built in.
It is not easy to design a robust system from scratch. You might start out nicely but then the requirements might change unexpectedly and you will have
tight deadlines to keep that will prevent you from doing proper refactoring.
Get a framework. Or if you already are working with one then before you get on with designing check what built in interfaces it offers!
Frameworks have usually decent documentation that includes a list of interfaces it offers. Examples:

+ [Laravel 5.1](https://laravel.com/api/5.1/interfaces.html)
+ [Zend 2](https://framework.zend.com/manual/2.4/en/index.html#zend-config)
+ [Symfony 2](http://api.symfony.com/2.8/interfaces.html)

One more advantage is that those interfaces are a result of a work of thousands of developers that had spent gazillions of hours perfecting them.

### Design patterns are good for training.
I will go through design patterns [later](##designpatterns-1) however when talking about interface segregation it is worth noting that if you do
need to build your own logic then you might find inspiration while going over the most popular design patterns. The more you will use them the easier it
will be for you to design efficient relations and interfaces even if those are something completely new.

## Dependency Inversion
For the purpose of explaining Dependency Inversion it is useful to be familiar with terms *high level module* and *low level module*.
+ High level module: It is the boss, chief, the general. It's job is to set a policies, define how everything should work together. In OOP the
high level modules are interfaces (rule how objects provide services) and abstract classes (rule how objects should work internally).
+ Low level module: The grunts, ordinary workers that actually do the hard work based on the policies set by the boss. These are the concrete
classes that either implement the interfaces or extend the abstract classes.

The general idea is that the ordinary workers should check if the objects they work with have the correct boss and his blessing. They should not
create a tight link with one particular worker, they should only care if the worker that comes implements a proper interface needed or extends
a correct abstract class (has correct competencies) and thus is able to do a certain type of a job. That way any worker under a certain boss will
do.

Same goes for OOP - an object should expect that it's dependencies implement a certain interface or extend a certain abstract class rather than
creating a tight coupling with a particular concrete object.

See the example below:
```
//file IDocumentInteraction.php
interface IDocumentInteraction
{
    public function append($dataToAppend)
}

//file TextDocument.php
class TextDocument implements IDocumentInteraction
{
    public function append($dataToAppend)
    {
        //some logic that appends the file with data
    }
}

//file SolidDocumentHandler.php
class SolidDocumentHandler
{
    private $document;

    public function __construct(IDocumentInteraction $document)
    {
        $this->document = $document;
    }

    public function appendDataInDocument($data)
    {
        $this->document->append($data);
    }
}

//file MessyDocumentHandler.php
class MessyDocumentHandler
{
    private $document;

    public function __construct(TextDocument $document)
    {
        $this->document = $document;
    }

    public function appendDataInDocument($data)
    {
        $this->document->append($data);
    }
}
```
The difference between the *SolidDocumentHandler* and *MessyDocumentHandler* is that the second one expects a concrete (low level module)
class instead of an object that extends a given interface (high level class). The solid one can basically work with any type of document object
that implements the *IDocumentInteraction* interface and thus is very re-usable. Even better it will also drive the development of the depending
object into a more maintainable manner and it will prevent you from using any methods of the dependency that are not part of the interface allowing for
nice encapsulation.

Some technical manuals might summarize the above like that:
> High-level modules should not depend on low-level modules. Both should depend on abstractions.
>
> Abstractions should not depend on details. Details should depend on abstractions.

In other words never use concrete classes inside abstract classes. Use abstractions whenever possible.

### Dependency Injection vs Dependency Inversion
It is easy to mix up the two. But it does not hurt much because these two are the best friends.

Dependency Inversion is the general concept to make classes require their dependencies to implement an interface or extend an abstract class while
Dependency Injection is the method in which you provide those dependencies.

### Type hinting
In PHP5 you can type hint objects and arrays in method interfaces:

```
    public function __construct(IDocumentInteraction $document)
    {
        $this->document = $document;
    }
```
The way *IDocumentInteraction* is used is called type hinting. Never forget to add it. It makes the code self-descriptive and easy to understand.

## Summary: SOLID
SOLID guidelines are meant to allow you to build a scaleable and maintainable object oriented code. SOLID requires the developer to do some extra
planning and put some extra effort into designing relations between objects however if done properly such investment is quickly earned back multiple
times over because it (greatly) shortens future development time. In other words SOLID helps prevent of adding of technical debt into your project.

The following make up the SOLID rules:
+ [Single Responsibility Principle](#singleresponsibility) - one class should have only one reason to change. In other words every change in the
system should require changes made to just one class that is handling that particular task. Bear in mind that management or creation of other
objects is also one such task. Allows for a loosely coupled system where parts can be easily re-used.
+ [Open/Closed Principle](#openclosedprinciple) - An interface needs to be *closed* for modification after being released. The objects
implementing it are however open for being extended or modified internally. This makes sure that any class that is dependent on another that
implements a given interface will not need the way it is using the interface ammended as well.
+ [Liskov Substitution](#liskovsubstitution) - states that any child class should not radically change the parent's behaviour so that objects
that depend on the parent can also always use it's children without breaking anything. This rule allows the parent to define the whole family
and what it can do and prevents confusion when the child does something unexpected.
+ [Interface Segregation](#interfacesegregation) - recommends segregating interfaces by specific functions that the implementing objects
should offer. An interface should contain only a small number of methods that are vital to achieving a particular task. Prevents the
creation of huge interfaces which might force the implementing objects to have methods that are nothing more than *placeholders* made to satisfy the
interface implementation requirements.
+ [Dependency Inversion](#dependencyinversion) - objects should define their dependencies by specifying an interface or an abstract class the dependency needs to
extend and not point toward a concrete class. That way objects can be made in a more reusable manner since they might accept a wide range of
concrete dependencies rather that allowing for just a concrete one.

# Good coding principles
Apart from the SOLID rules there exist also some coding principles that serve the purpose of guiding a developer to write better code or simply to make
it easier for the developer to collaborate with other developers which is a great advantage in any large project.

## Don't Repeat Yourself
Every decent developer will smile at the statement that being a developer is about being proficient at copy-pasting. But one have to remember that
this refers to the ability of finding the right solution [somewhere](#extradonotreinventthewheel) rather than copying it over from inside
the code base.

If you copy-paste code within your very own codebase with occasional tiny modifications then you got the *good bit* about copy-pasting wrong. Rather than
this being a virtue it just means you are being lazy and are creating a mess someone else will probably need to clean up after you if it will be
spotted in time.

If you copy-paste anything inside your own code base then there are high chances that when you will need to refactor this area you will have to do
that in two places now. Or more. Instead take a look at the bit you want to copy - and try to make it more parameterizable so it can be re-used.

### Repeating of responsibilities
This is the *higher level* of copy-pasting within you own code base. In here you do not duplicate the code itself but rather the general functionality. For example
when you need to do something but the class that normally does that is a huge and complex monolith then rather than checking the class' methods and inner
workings and re-using those you would write a new one that have some part of the original class' logic. Because it's faster.

However like with copy-pasting of the code - doing things in such a way might mean that the next time you will have to do refactoring in two or more places
not to mention that it will get confusing as to which class to use in the future.

## Cognitive load
Before you start working with a piece of code you first need to go through it and understand what it is doing. You have to sort of *load it into RAM* inside
your brain first. This can sometimes take most of the time required to deliver a solution.

Everything in this document is about making it easier for the developer to understand and modify the code from architectural perspective but
there are also things that are very helpful yet might seem too trivial at first to be even considered.

### Coding standards
One of the most underestimated little things that greatly speed up development in a team based environments are the coding standards.
These are the rules of how your code looks and do not care about the functionality. Consider the two examples below:

```
if ( -- some condition -- ) {
    //some code
} else {
    //some code
}
```

```
if ( -- some condition -- )
{
    //some code
}
else
{
    //some code
}
```

Both examples are a perfectly valid code. The way you yourself structure the if/else statements is probably dependent on the tutorials you have used
when you were learning to code, which code snippets you have built your first programs with and some personal experimentation. It became a habit of yours
to structure the code in a specific way and you do that because your brain is used to this. Any other structure will create a brief confusion for your
cognitive processes and if the code is littered with many different coding styles then it can really wear one down quickly.

It is a popular argument against adjusting to a different coding standard that the one you are using is *more clear*. And one will always have a gazillion
or arguments to support it. However as somebody who had his own style once and then then had to forcibly switch to [another one](#psr) after getting a new
job  I can with all confidence say that it just does not matter. Every style will become *more clear* if you use it long enough and you will eventually forget
about the old one (or even some day wonder why you ever did things in such an awful way).

Coding standards might look like unnecessary for junior developers that are still learning the basics but most companies enforce some kind of a
standard today. It is best to simply let go of the personal habits as soon as possible and adjust to the new ones. It might take a month or two but
if you intend to work in the company you work in any longer then it is worth it as it will save a lot of work that your brain has to do.

If a development team share one coding standard then a portion of cognitive load simply disappears which in the end saves money.

#### PSR
[This](http://www.php-fig.org/psr/) is the most popular coding standard in the world of PHP supported by [PHP-FIG](http://www.php-fig.org/). Every major
framework and library has either already implemented this standard or will implement it in the near future as it is slowly becoming the *de facto* industry standard.

Currently the best thing that can happen when it comes to coding standards is that your company is using the PSR coding standard. It is the most future proof
one and once you make it into your own habit then you will probably never have to switch into something different again. Additional benefit is that most of the
modern third party code and the tutorials online are going to be using PSR and all other coding styles will get faded out.

It is worth to note that only the two PSR recommendations refer to the coding styles - that is [PSR-1](http://www.php-fig.org/psr/psr-1/) and
[PSR-2](http://www.php-fig.org/psr/psr-2/). The second one is an extension to the first one made some time earlier. At the time of writing this there
is also a draft PSR-12 recommendation but you should wait until it is 'Accepted' before you adopt it since it might still change. The PSR-12 is also meant to
extend the previous two recommendations.

All other recommendations do not refer to the coding standards but are also useful especially is you are creating code that you intend to release into the
public so it is compatible with frameworks that support PHP-FIG.

Many of the recommendations were established after some long, fierce battles made between camps of developers that would support one way of doing things or
another. Then in the end they would vote and some solution would get democratically accepted. In general I would trust those guys that they know what they are doing.

### Clever, compressed code
First consider the following example:

```
public function orderPizza($size)
{
    return $this->restaurant->hasPizza($this->getFavouritePizza($this->session->getUser()->getId())->getId()) ?
    ($this->restaurant->processPayment(
        $this->restaurant->getPizza($this->getFavouritePizza($this->session->getUser()->getId())->getId()),
        $this->session->getUser()->getPaymentProcessor())
    ? true : false)
    :
    false;
}
```

And now this one:

```
public function orderPizza($size)
{
    $currentUser    = $this->session->getUser();
    $favouritePizza = $this->getFavouritePizza($currentUser->getId());

    if ($this->restaurant->hasPizza($favouritePizza->getId())) {
        $selectedPizza    = $this->restaurant->getPizza($favouritePizza->getId());
        $paymentProcessor = $currentUser->getPaymentProcessor();

        if ($this->restaurant->processPayment($selectedPizza, $paymentProcessor)) {
            return true;
        }
    }
    return false;
}
```

Which one is easier to read and comprehend? I am betting on the second one. It does things in small iterations and is naming the results of those
operations so it is easy to follow what is going on.

The first example is a compressed code. Both examples do the same logic but the first one has been done by a developer that is a little crazy about
*optimization* or likes when his/her code appears to be *professional*. Unfortunately a compressed code is much harder to read and maintain. Debugging of
the first example means that every action happens on the same line  in the file from the debugging point of view so it is harder to pinpoint where an error
happens when it does.

Compression is only useful when you need to send the code somewhere like over narrow bandwidth - but there are tools like *minifiers* for that. Also note
that in most cases the PHP engine only parses the code once and then it stores it in cache so the extra variable declarations do not cost much and memory
is not a problem today. In the end code compression is like shooting yourself in the foot - you want optimization but all you get is more costly
maintenance of the code. Compressed code also discourages other developers from properly going over the code and understanding what it does so they are
more likely to start inventing new things rather than re-use or refactor the compressed things.

Things get even more nasty if the developer wants to show his skills by producing the *clever* code. A *clever* code is when some things that can be easily
done by using a conventional and simple approach but get done in an unconventional way. Usually the author simply wants to show off that he/she is able to use some not
very often used feature of the programming language that appears initially to be a very smart piece of engineering but in fact is just garbage that adds unnecessary
confusion.

## Documentation, doc-blocks, in-line comments
It is a great habit to explain what the code you have just cooked does. The documentation can have many forms:
* a wiki or [Confluence](https://www.atlassian.com/software/confluence) styled site that describes how things work in your application,
* *docblocks* over your classes and methods,
* inline comments next to more complex blocks of code.

A well maintained site that documents your application is a salvation that can save a lot of explaining, reduce the amount of duplicated code and in general
enforce some sort of organization in the project. The drawbacks are it needs to be maintained alongside the code but if done properly I believe the pros well
outweigh the cons.

One must also consider the fact that there are people that just do not work well with written text and prefer verbal communication. For those having to
maintain the documentation will be a nightmare and if your team consists many of such people then you are out of luck as it will just not work.

*Docblocks* are comments that you put usually in front of every class and method to describe what they do. This is the bare minimum that you should always
add to any code you make. There exists coding standards for *Docblocks* and it is good to follow them as they help you in making sure that you cover all
important aspect of how a given class or method works. A good reference of how to make good *docblocks* can be found [here](https://www.phpdoc.org/docs/latest/index.html).

### PHPDocumentor
[This](https://www.phpdoc.org/) tool allows you to generate documentation for your project automatically. The only requirement is that you have properly formed
*docblocks* inside your code that the PHPDocumentor parses and creates pages with information for.

### Focus on the encapsulated functionality, not what is using it
Whether you are adding a *docblock* to a class or method that already exist or you are creating a new one it is very possible that you might want
to add some explanation for the next guy that comes across how you used that class or method in the consuming code. That is because at that time
you are thinking about the given functionality from the context of the code that is using that functionality.

Good thinking, however this also breaks [encapsulation](#encapsulation). A class or method should never care about the code that calls it and so
the *docblock* should not as well. Always explain only the logic that is happening inside the class or method - that way the explanations you will make will
be *loosely coupled* to the rest of the code base and encourage re-usability.

There are some tags that allow you to reference other code like *@uses*, or *@used-by* but those should be used sparingly and only in cases where the
description of a relation is really vital.

## Variable and method naming
When creating names for the variables make sure they describe what they hold in the context of the overall logic of the code around them rather than them
describing the type of the value they hold. If you are naming variables by type then it might get easy to mix them up once many variables holding the same type
of data are present in the code.

A method name should be a super quick and convenient explanation of what the logic they encapsulate does. That way it is much easier to iterate over the code that
is calling them - you should not be forced to navigate to the method and read it's *docblock* to know what is happening every time.

## Summary: Good coding principles
* [Don't Repeat Yourself](#dontrepeatyourself) - Try not to copy-paste any code within the code base. The same includes the responsibilities of the classes in the project.
Any such duplication means that the effort required to maintain it will also double.
* [Cognitive Load](#cognitiveload) - Write code that is easy to understand, follows a code standard and is not compressed or clever. These are tiny things that seem not
very important but can really make a big difference.
* [Documentation](#documentationdocblocksinlinecomments) - Document a lot and encourage others to document the code they make. Documentation costs but when being reasonable
it really provides a great returns of the invested time in a self-explanatory code.
* [Variable and method naming](#variableandmethodnaming) - When naming variables scope out your focus the the general logic around the variable. When naming methods make
sure they quickly and efficiently explain the logic they encapsulate.

# Extra: *Do not reinvent the wheel!*
We did not become developers to do repetitive and boring things. We became developers because we love to tinker, we love to build and see how
things we make turn the world into a better place. We also want to be recognized and praised for our work since we have spent so much time and energy
into learning how to do programming. We see problems as challenges and it is easy for us to think that the measure of how good one is at doing
his/her job is if he/she is able to single-handedly tackle and obliterate the problem now matter how big it is. So we immediately start thinking on how to
go from A to B using only our own knowledge and experience and we carry on to invent a genius contraption that can do all the things in the world and
that is supposed to leave everyone around in awe.

Stop doing that. Seriously.

Whatever you have thought of has already been done. Many times over. And is possibly sitting just under your nose in the framework and/or libraries you are using
or is a few clicks away if you do just a little research.

I believe the best developers see the interest of the business or organization they work for first rather than treat the code base as their personal sandbox where
they can have fun and experiment a little. And the interest of the business is to have a maintainable code where you can have a rapid release cycle rather than a
turtle pace. This can only be achieved if you re-use things as much as possible and do only a minimum of development - just enough to make all the pieces work together.

Take for example the gaming industry - let's say you want to make an FPS game. Would you buy an engine and a bunch of technologies and focus just on adding some
content or will you design your game from scratch? The first approach takes about 2-3 years for AAA products while the second more than 50. That is how much time has
passed since the first computer games were made. What we play today inherits ideas developed over decades. Same principles work for PHP applications.

Stay informed with the state of the platform you use and learn to re-use others work and you will be a king!

## over-engineering
When you build a new feature make sure you do it strictly in accordance with the requirements. It is very easy when you know your system well (or the total opposite - you are
new and want to impress) to fall under the influence of the little devil inside your head and add a little more, because it just makes sense and it looks like it would
be very useful. Never do that.

The more extra features you pour in the less flexible that feature becomes (surprise!). That is because there is simply more code that needs more time to be understood
and you have taken away the ability to design and add more functionality later. You will also try to make use of the functionality you have *foreseen* will be useful to
handle any new requirements that will come rather than designing a proper, simple and direct solution. This leads into a lot of overriding rather than extending and is a
perfect recipe for an awful and unmaintainable code base. The more code you write the more code changes you might have to do in the future. The only case this can be useful
to you is when you want to make your organization heavily dependent on you because only you can understand the things you make.

Also try not to over-interpret the requirements. If some customization is not explicitly required - do not implement it - go the most efficient and simple way.

>You aren't gonna need it

Or *YAGNI* is in fact a well known rule in [extreme programming](https://en.wikipedia.org/wiki/Extreme_programming). Over-inflation with functionality breaks any intentions of
having a rapid development cycle.

Another disadvantage of over-engineering is that the extra features you made might actually never be used! Chances are that the extra hours or even days of coding will
be simply wasted (which directly translates to wasted money).

---

Author: Radosław Kurowski [radix@salvilines.eu](mailto:radix@salvilines.eu), last update: 13.06.2017

![PHP Logo](https://upload.wikimedia.org/wikipedia/commons/3/31/Webysther_20160423_-_Elephpant.svg "PHP Logo")
