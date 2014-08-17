---
layout: post
title:  "Testing doubles - mocks and stubbing"
date:   2014-08-16 23:00:00
---

In well designed software each class will have a single responsibility. However, in software systems, the various classes that make up the system will need to interact with each other. When test-driving the code for each class, these interactions will need to be taken into account. The Chicago school, also known as the classical school, tests these interactions by creating real instances of each class. There are several problems that can arise as a result of using real instances of other classes in tests. These problems are easiest illustrated with an example, alongside the alternative approach of using doubles as advocated by the London school. The purpose of using doubles in testing is much like the reason why stunt doubles are used in films. Stunt doubles are used to undertake dangerous or risky parts of films, in which it is not necessary for the credibility of the film to have the real actor. Likewise, doubles are used in tests because it is not necessary for the validity of our unit tests to ensure that the interactions between our various classes work in a particular way. We just want to test that they happen. 

So let's begin our example. I'll talk you through the creation of a simple software system that allows you to borrow books from a library. To start with, I would write out a simple description of my system in order to identify the various classes that I will need to create. 

Description: we are building a system that manages *books* that can be borrowed by *people* from a *library* and returned after they have been read. The books can be lost when they are in the user's possession, in which case they will not be available for further borrowing.

I have italicised all the nouns in my description, as I will take these as my starting point for my classes. Say I am working collaboratively on this project, and it has been decided that I will create the person class, whilst another member of the team will start to work on the book class. 

Let's start thinking about our person class in terms of what responsibilities the person will have. When writing my first test, I always want to start with the simplest scenario: a person can have a book. In my first test, I would expect that upon initialisation, a person doesn't have a book. Let's write our test. 

{% highlight ruby %}
it 'should not have a book upon initialisation' do 
	hannah = Person.new
	expect(hannah).not_to have_book
end 
{% endhighlight %} 

RSpec will complain at me that there is no method has_book?

So let's go ahead and create it

{% highlight ruby %}
def has_book?
end
{% endhighlight %} 

The test still fails because it expected 'false' but received 'nil'. The simplest way to make this test pass would be to pass in the value false. Baby steps, remember. 

Our method is not yet robust enough as it doesn't actually account for the responsibility that we want it to. The next step therefore would be to write another test.

{% highlight ruby %}
it 'should have a book when given a book' do 
	hannah = Person.new(:book)
	expect(hannah).to have_book
end 
{% endhighlight %} 

Let's just have a closer look at what we did there. This is our first use of mocking. We gave the person a book as a symbol. This is not a real instance of the book, in reality we could put anything we like there. It doesn't even have to be a symbol. We are just testing that the person receives *something*. We have made it a symbol of a book to remind ourselves, and the people that we are working with, that once the system is wired together, we will ensure that a person can only borrow a book and not some other class. So why did we mock this instead of checking whether the person received a real book? **We want to avoid pollution in our code.** As an analogy, if we were testing how a particular gas behaved, we would test it in a vacuum rather than in air. If we tested it in the air, the behaviour would be obscured by its interactions with oxygen, nitrogen and other elements. So too with our code. We want to test our person class in isolation, to ensure that the person behaves as it should do. There could be errors in the code base of the book class which obscure the behaviour of our person class if we use a real instance of a book. By keeping each class separate we can test that each class behaves as it should and thus debugging becomes far more manageable. Moreover, if we were not using doubles at this point, I would have to go and create my book class and develop it up to the point where the interaction could occur. This would make working independently all the more difficult.  

Now RSpec will complain to us that there are the wrong number of arguments. It expected zero arguments, but received one.  We can fix this by initialising our Person class with a book. 

{% highlight ruby %}
def initialise(book=nil)
	@book = book
end 

def has_book?
	!@book.nil?
end 
{% endhighlight %} 

Here we have initialised our person with a book, and set the default value to nil, so that a person doesn't have a book when initialised, unless we give her one. Now both our tests our passing.

Our next step might be to design the code for borrowing of the books from the library. 

{% highlight ruby %}
it 'should be able to borrow a book from the library' do 
	library = double :library
	hannah = Person.new(:bike)
	expect(library).to receive(:lend_book)
	hannah.borrow_book_from(library)
end 
{% endhighlight %} 

And our code to make it pass would look something like this.

{% highlight ruby %}
def borrow_book_from(library)
	library.lend_book
end 
{% endhighlight %} 

So what is going on here? We don't yet have a 'lend_book' method in our programme anywhere, so how is the code passing? What is happening in this code is pure design. We are designing and shaping how our person is going to interact with the book, because we don't yet have a book. Pretty neat that we can design our person class and its interactions with other objects without having yet created those objects, no? Using doubles has allowed us to write our code in a methodological manner where we don't have to keep jumping back and forth between classes.  

Our code is not yet complete. Although our person can borrow a book from the library, another event needs to happen. Once the book has been borrowed, we want the person to then have the book. So let's write another test to ensure that our method encapsulates its full responsibility:

{% highlight ruby %}
it 'should have a book after borrowing it from the library' do 
	library = double :library, lend_book: :book
	hannah = Person.new(:bike)
	hannah.borrow_book_from(library)
	expect(hannah).to have_book
end 
{% endhighlight %} 

The first line of our test is interesting. We can pass our double a hash of methods as the key, and their return values as the value. This is because we don't expect anything here. We just want to check for its presence, that it is there. We have already tested that this method has been called. Alternatively there is a more verbose way it could be written:

{% highlight ruby %}
allow(library).to receive(:lend_book).and_return(:book)
{% endhighlight %} 

So our test now expects our person to have a book, once she has borrowed it. 

To make our test pass: 

{% highlight ruby %}
@book = library.lend_book
{% endhighlight %} 

Why does this make our test pass? The answer lies in the fact that when we call the method lend_book on the library, the library will return a book to the person. The book that has been lent is now the book that is possessed by the person, and is thus the instance variable of book. 

And there you have it. 

In summary there are three main advantages to using doubles:
1. We can test the integrity of the class without being concerned that some of the behaviour is being cause by interactions with other classes. 
2. We can design how our various classes interact without having to create them all at once. 
3. Developers can work in a methodological manner, independently 

Hannah :) 
