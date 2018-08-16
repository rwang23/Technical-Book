##Builder

###Motivation
- When construction gets a little complicated
- some objects are simple and can be created in a single contructor call
- other objects requrie a lot of ceremony to create
- having an object with 10 constructor arguments is not productive
- Instead, opt for piecewise construction
- Builder provide an API for doing this
- 学会拆分builder,不要把一个Builder弄太复杂，不然很难扩展

###Main function
- 对比一下main function的不同
- 再没有Builder前，完全通过一步步的append
- 建立了builder后，只需要传入nodeName和nodeText
- fluent builder可以实现chain call

```java
public static void main(String[] args)
  {


    // we want to build a simple HTML paragraph
    System.out.println("Testing");
    String hello = "hello";
    System.out.println("<p>" + hello + "</p>");

    // now we want to build a list with 2 words
    String [] words = {"hello", "world"};
    StringBuilder sb = new StringBuilder();
    sb.append("<ul>\n");
    for (String word: words)
    {
      // indentation management, line breaks and other evils
      sb.append(String.format("  <li>%s</li>\n", word));
    }
    sb.append("</ul>");
    System.out.println(sb);

    // ordinary non-fluent builder
    HtmlBuilder builder = new HtmlBuilder("ul");
    builder.addChild("li", "hello");
    builder.addChild("li", "world");
    System.out.println(builder);

    // fluent builder
    builder.clear();
    builder.addChildFluent("li", "hello")
      .addChildFluent("li", "world");
    System.out.println(builder);
  }
```

###Multiple Builder
####Builder Facade
- 如果一个object，太复杂了，太多初始化了，就可以用这种subbuilder，这样就能从一个subbuilder到另一个subbuilder
- main函数.这个真的厉害，chain call就构造出了一个Person Object

```java
class PersonBuilder
{
  // the object we're going to build
  protected Person person = new Person(); // reference!

  public PersonJobBuilder works()
  {
    return new PersonJobBuilder(person);
  }

  public PersonAddressBuilder lives()
  {
    return new PersonAddressBuilder(person);
  }

  public Person build()
  {
    return person;
  }
}

class PersonAddressBuilder extends PersonBuilder
{
  public PersonAddressBuilder(Person person)
  {
    this.person = person;
  }

  public PersonAddressBuilder at(String streetAddress)
  {
    person.streetAddress = streetAddress;
    return this;
  }

  public PersonAddressBuilder withPostcode(String postcode)
  {
    person.postcode = postcode;
    return this;
  }

  public PersonAddressBuilder in(String city)
  {
    person.city = city;
    return this;
  }
}

class PersonJobBuilder extends PersonBuilder
{
  public PersonJobBuilder(Person person)
  {
    this.person = person;
  }

  public PersonJobBuilder at(String companyName)
  {
    person.companyName = companyName;
    return this;
  }

  public PersonJobBuilder asA(String position)
  {
    person.position = position;
    return this;
  }

  public PersonJobBuilder earning(int annualIncome)
  {
    person.annualIncome = annualIncome;
    return this;
  }
}

class BuilderFacetsDemo
{
  public static void main(String[] args)
  {
    PersonBuilder pb = new PersonBuilder();
    Person person = pb
      .lives()
        .at("123 London Road")
        .in("London")
        .withPostcode("SW12BC")
      .works()
        .at("Fabrikam")
        .asA("Engineer")
        .earning(123000)
      .build();
    System.out.println(person);
  }
}
```
