Designing Business logic
------------------------

OO paradigm: Objects as a main piece of decompsition
	
	1/ Controling the change
	-------------------------
	<:> Think on term of ADTs : Types that are defined operationally as opposed to structurally
		ADT exemples : a class definition where all data members are have been declared privte
			       an even BETTER exemple : a java intertace (java 8 ???) 
	<:> String data encapsulation : prevention of access to data defined in a class(???) from outside of the class 
		>>>>>> improve the reseliency of programs to CHANGES by localizing the EFFECTS of changes 
		>>>>>> OO gives us the tools to CONTROL the change

		>>>>>> Data exhibition phobia : principle like (tell don't ask) becomes quickly dogma that prevent the deveolleper to think
						differenty when the nature of the problem he is trying to solve changes
						At a certin limit we will need to present the data
							thinkin that the objet as the owner of data is also responsable of it presentation IS A BAD idea
							presentation logic changes : mobile, desktop, markets, sspecific customer groups presentations
							What if we think that we expose the result of the computation
							In the presentation layer we need informations (the result of data processing) NOT to change but to PRESENT
							


							good knowledge of the OO use boundaries

						in other words, OO is not the best tool for every problem domain
						(The writeInto phenomenon => exponential incease of verbosity)
						We could say that "The problem iss not on the OO style but on the bad usage in where it s not suitable for."

	

	2/ Extensibility
	----------------
		Expression Problem
	
	3/ Concurency
	----------------
		=> Threads + sychronization :: Another layer of complexity to manage
		=> immutablity : thinking in term of data transformations
			=> Can OO style let us think about transformation without pain ???



Functional paradigm: Function as a first class citizen and the main piece of decomposition + immutabity
	>> NO CHANGE TO CONTROL thanks to immutability anstead we think about TRANSFORMATIONS
	>> NO data exhibition phobia


Imperative paradigm




Beans (POJO) oriented paradigm (OO + AOP)
  transactions
  logging
  security
  life cycle management
  dependency injection ??
  Remoting
  ?monitoring
  ?pooling
	=> A programming model that let us dont care about technology but focus in business logic
	=> Spring promotes good design practices:
		<:> Dependency injection for loose coupling
		<:> AOP for handling the cross cutting concerns
			=> But you must decide how to structure your business logic
				<:> Domain model pattern - OO
				<:> Transaction Script pattern - Procedural

  Statelesss & statefull beans ??
  What about the OO principles, (encapsulation, ...) is it still valid for this style ?
  Is the OO the only possible building base that can make beans oriented programming POSSIBLE ??
  Can we build a bean model based in functions ??



--------
(Ref 1 : http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.79.4719&rep=rep1&type=pdf)

